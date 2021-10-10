
1) приводим файлы в первоначальынй вид

	а) app.component.html

		<!--The content below is only a placeholder and can be replaced.-->
		<div>
		  <h1>
		    Todo {{ title }}
		  </h1>
		</div>

	б) app.component.ts

		import { Component } from "@angular/core";

		@Component({
		  selector: "app-root",
		  templateUrl: "./app.component.html",
		  styleUrls: ["./app.component.css"]
		})
		export class AppComponent {
		  title = "Angular";
		}

2) создадим кнопку добавления новой задачи
	а) файл app.components.ts


	<div>
	  <h1>Todo {{ title }}</h1>
	  <input type="text" placeholder="Enter new Task" #task />
	  <br />
	  <br />
	  <button>Add new Task</button>
	</div>

3) определим функцию, которая будет вызываться при клике на кнопку

	<div>
	  <h1>Todo {{ title }}</h1>
	  <input type="text" placeholder="Enter new Task" #task />
	  <br />
	  <br />
	  <button (click)="addTask(task.value)" >Add new Task</button>
	</div>

4) создадим функцию обработки кнопки
	а) app.components.ts

	import { Component } from "@angular/core";

	@Component({
	  selector: "app-root",
	  templateUrl: "./app.component.html",
	  styleUrls: ["./app.component.css"]
	})
	export class AppComponent {
	  title = "Angular";

	  addTask(item: string) {
	    console.warn(item);            // просто вывод сообщения...
	  }
	}	

5) сделаем добавление данных в список, каждое данное состоит из двух полей
	а) id = число записей
	б) name = присланный текст

	  list: any[] = [];

	  addTask(item: string) {
	    this.list.push({
	      id: this.list.length,
	      name: item
	    });
	    console.warn(this.list);
	  }

6) сделаем вывод записей ниже кнопки

	<div>
	  <h1>Todo {{ title }}</h1>
	  <input type="text" placeholder="Enter new Task" #task />
	  <br />
	  <br />
	  <button (click)="addTask(task.value)">Add new Task</button>
	  <br />
	  <br />
	  <ul *ngFor="let item of list">
	    <li>{{ item.name }}</li>
	  </ul>
	</div>


7) добавим после каждого названия задачи кнопку для удаления задачи

  <ul *ngFor="let item of list">
    <li>{{ item.name }} <button>Remove</button></li>
  </ul>

8) напишем обработку для данной кнопки

  <ul *ngFor="let item of list">
    <li>{{ item.name }} <button (click)="removeTask(item.id)">Remove</button></li>
  </ul>

9) напишем функцию
	а) app.compomemts.ts

	import { Component } from "@angular/core";

	@Component({
	  selector: "app-root",
	  templateUrl: "./app.component.html",
	  styleUrls: ["./app.component.css"]
	})
	export class AppComponent {
	  title = "Angular";
	  list: any[] = [];

	  addTask(item: string) {
	    this.list.push({
	      id: this.list.length,
	      name: item
	    });
	    console.warn(this.list);
	  }

	  removeTask(id: number) {             // вот это...
	    console.warn(id);
	  }
	}

10) реализация через фильтр

  removeTask(id: number) {
    this.list = this.list.filter((item) => item.id !== id);
  }