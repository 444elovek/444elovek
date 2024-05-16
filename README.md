<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Страница 1</title>
</head>
<body>
    <h1>Страница 1</h1>
    <form id="form1">
        <textarea id="ideas1" placeholder="Введите ваши идеи, каждую с новой строки"></textarea>
        <button type="submit">Отправить</button>
    </form>
    <h2>Ваши идеи на этой странице:</h2>
    <ul id="ideasList1"></ul>
    <script>
        document.getElementById("form1").addEventListener("submit", function(event) {
            event.preventDefault();
            let ideas = document.getElementById("ideas1").value.split("\n");
            ideas.forEach(function(idea) {
                localStorage.setItem("1_" + Date.now(), idea.trim());
            });
            displayIdeas("ideasList1");
            setTimeout(() => {
                window.location.href = "page2.html";
            }, 10000);
        });

        function displayIdeas(listId) {
            let ideasList = document.getElementById(listId);
            ideasList.innerHTML = "";
            for (let i = 0; i < localStorage.length; i++) {
                let key = localStorage.key(i);
                let value = localStorage.getItem(key);
                if (key !== null && key.startsWith("1_")) {
                    let listItem = document.createElement("li");
                    listItem.textContent = value;
                    ideasList.appendChild(listItem);
                }
            }
        }
        displayIdeas("ideasList1");
    </script>
</body>
</html>
