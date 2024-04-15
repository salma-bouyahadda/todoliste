<!DOCTYPE html> 
<html lang="fr"> 
<head> 
<meta charset="UTF-8"> 
<title>Todo List</title> 
<style> 
body {
    font-family: Arial, sans-serif;
    background-color: #f0f0f0;
    padding: 20px;
}

h2 {
    color: #333;
    margin-bottom: 20px;
}

#todoList {
    background-color: #fff;
    border-radius: 5px;
    padding: 20px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

.task {
    margin: 10px 0;
    padding: 15px;
    background-color: #e9e9e9;
    border-radius: 5px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    border-left: 5px solid #09c838;
}

.task.completed {
    background-color: #dcdcdc;
    border-left: 5px solid #d20e00;
}

.task button {
    padding: 8px 15px;
    border: none;
    border-radius: 3px;
    cursor: pointer;
    transition: background-color 0.3s ease;
}

.task button:hover {
    background-color: #0f8ec4;
    color: #fff;
}

#newTask {
    padding: 10px;
    width: 60%;
    border-radius: 3px;
    border: 1px solid #ccc;
}

#addTask {
    padding: 10px 15px;
    border: none;
    border-radius: 3px;
    cursor: pointer;
    background-color: #3498db;
    color: #fff;
    transition: background-color 0.3s ease;
}

#addTask:hover {
    background-color: #2980b9;
}


</style> 
</head> 
<body> 

<h2>Ma liste de tâches</h2> 

<div id="todoList"> 
<!-- Exemple de tâche --> 
<div class="task" data-task-id="1"> 
<span>Faire les courses</span> 
<div> 
<button class="completeTask">Accomplir</button> 
<button class="deleteTask">Supprimer</button> 
</div> 
</div> 
<!-- Les tâches suivantes seront ajoutées ici --> 
</div> 

<h2>Ajouter une nouvelle tâche</h2>
<div>
    <input type="text" id="newTask" placeholder="Nouvelle tâche...">
    <button id="addTask">Ajouter</button>
</div>

<script> 
document.addEventListener("DOMContentLoaded", function() {
    const todoList = document.getElementById("todoList");
    const addTaskButton = document.getElementById("addTask");
    const newTaskInput = document.getElementById("newTask");

    addTaskButton.addEventListener("click", function() {
        const taskName = newTaskInput.value;
        if (taskName.trim() !== "") {
            addNewTask(taskName);
            newTaskInput.value = "";
        }
    });

    todoList.addEventListener("click", function(event) {
        if (event.target.classList.contains("completeTask")) {
            toggleTaskComplete(event.target.parentElement.parentElement);
        }

        if (event.target.classList.contains("deleteTask")) {
            deleteTask(event.target.parentElement.parentElement);
        }
    });

    function toggleTaskComplete(taskElement) {
        taskElement.classList.toggle("completed");
    }

    function deleteTask(taskElement) {
        taskElement.remove();
    }

    function addNewTask(taskName) {
        const taskId = Date.now(); // Utilisation de la date actuelle comme ID unique
        const newTask = `
        <div class="task" data-task-id="${taskId}">
                <span>${taskName}</span>
                <div>
                    <button class="completeTask">Accomplir</button>
                    <button class="deleteTask">Supprimer</button>
                </div>
            </div>
        `;   
        todoList.insertAdjacentHTML("beforeend", newTask);
    }
});
</script> 

</body> 
</html>
