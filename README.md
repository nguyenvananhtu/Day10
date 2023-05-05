<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8" />
		<meta http-equiv="X-UA-Compatible" content="IE=edge" />
		<meta name="viewport" content="width=device-width, initial-scale=1.0" />
		<title>Day10</title>
		<link
			rel="stylesheet"
			href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta2/css/all.min.css"
			integrity="sha512-YWzhKL2whUzgiheMoBFwW8CKV4qpHQAEuvilg9FAn5VJUDwKZZxkJNuGM4XkWuk94WCrrwslk8yWNGmY1EduTA=="
			crossorigin="anonymous"
			referrerpolicy="no-referrer"
		/>
		<link rel="stylesheet" href="style.css" />
	</head>
        <style>
            * {
	padding: 0;
	margin: 0;
	font-family: sans-serif;
	box-sizing: border-box;
}

body {
	background: linear-gradient(to right, #fae43e, #859ef0);
	min-height: 100vh;
}

.container {
	width: 400px;
	background-color: #fff;
	margin: 100px auto;
	border-radius: 5px;
}

.form {
	padding: 10px 20px 10px 0;
	display: flex;
	align-items: center;
	justify-content: space-between;
	border-bottom: 1px solid #aaa;
    
}

.form input {
	outline: none;
	border: none;
	padding: 0 20px;
	font-size: 24px;
	color: #444;
	width: 100%;
    
}

.form button {
	outline: none;
	border: none;
	background-color: rgb(101, 103, 105);
	padding: 5px 15px;
	border-radius: 6px;
	cursor: pointer;
	color: white;
	font-size: 20px;
}
.form button:hover{
	background: linear-gradient(to right, #fae43e, #859ef0);   
}

.todos {
	padding: 0;
	margin: 0;
	list-style-type: none;
}

.todos li {
	border-top: 1px solid #e5e5e5;
	cursor: pointer;
	font-size: 22px;
	padding: 15px 22px;
	display: flex;
	align-items: center;
    justify-content: space-between;
}

.todos li i {
	color: #aaa;
	opacity: 0.4;
}

.todos li:hover i {
	opacity: 1;
}

.todos li span {
	overflow: hidden;
	text-overflow: ellipsis;
	padding-right: 10px;
}

.todos li.completed span {
	color: #b6b6b6;
	text-decoration: line-through;
}
.todos li img{
    width: 40px;
    height: 40px;
    margin-left: 10px;
}

        </style>
	<body>
		<div class="container">
			<form class="form">
				<input type="text" placeholder="search..." />
				<button>Add</button>
			</form>
			<ul class="todos"></ul>
		</div>

		<script>
            const input = document.querySelector('form input')
const ul = document.querySelector('.todos')
const form = document.querySelector('form')

const todos = JSON.parse(localStorage.getItem('todos'))

if (todos) {
	todos.forEach((todo) => addTodo(todo))
}

function addTodo(todo) {
	const li = document.createElement('li')

	li.setAttribute('class', todo.completed ? 'completed' : '')
	li.innerHTML = `
        <img src="https://vnn-imgs-f.vgcloud.vn/2019/04/24/10/top-10-moto-nhanh-nhat-nam-2019.jpg" alt="">
        <span>${todo.text}</span>
        <i class="fas fa-trash"></i>
    `

	li.addEventListener('click', function () {
		this.classList.toggle('completed')
		updateTodos()
	})

	li.querySelector('i').addEventListener('click', (e) => {
		e.target.parentElement.remove()
		updateTodos()
	})

	ul.appendChild(li)
	updateTodos()
}

form.addEventListener('submit', (e) => {
	e.preventDefault()
	const text = input.value.trim()
	text != '' ? addTodo({ text, completed: false }) : undefined
	input.value = ''
})

function updateTodos() {
	const list = document.querySelectorAll('li')

	const todos = []

	list.forEach((item) => {
		todos.push({
			text: item.querySelector('span').innerHTML,
			completed: item.classList.contains('completed'),
		})
	})

	localStorage.setItem('todos', JSON.stringify(todos))
}

        </script>
	</body>
</html>
