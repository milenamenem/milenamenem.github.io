<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Lista de Músicas</title>
    <style>
        body {
            font-family: 'Roboto Rounded', sans-serif;
            margin: 0;
            padding: 0;
            display: flex;
            flex-direction: column;
            align-items: center;
            background-color: #000;
            color: #fff;
        }

        header {
            background-color: rgb(90, 15, 15);
            color: white;
            padding: 1em;
            width: 100%;
            text-align: center;
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        header img {
            width: 50px;
            height: 50px;
            margin-right: 0.5em;
        }

        header div {
            display: flex;
            align-items: center;
        }

        main {
            padding: 1em;
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 1em;
        }

        section {
            border: 1px solid rgb(172, 127, 127);
            padding: 1em;
            width: 300px;
            background: rgb(179, 76, 76);
            color: #000;
        }

        form {
            display: flex;
            flex-direction: column;
            gap: 0.5em;
        }

        ul {
            list-style-type: none;
            padding: 0;
        }

        li {
            display: flex;
            flex-direction: column;
            align-items: flex-start;
            gap: 0.5em;
            margin: 0.5em 0;
            cursor: pointer;
            padding: 0.5em;
            border: 1px solid #ddd;
            background: #fff;
            color: #000;
            border-radius: 5px;
        }

        li:hover {
            background: #f0f0f0;
        }

        .item-header {
            display: flex;
            justify-content: space-between;
            width: 100%;
        }

        .item-details {
            display: none;
            flex-direction: column;
            gap: 0.5em;
            border-top: 1px solid #ddd;
            padding-top: 0.5em;
            margin-top: 0.5em;
            width: 100%;
        }

        .item-details img {
            width: 100px;
            height: 100px;
            object-fit: cover;
        }

        .item-details p {
            margin: 0;
        }

        button {
            cursor: pointer;
        }
    </style>
</head>
<body>
    <header>
        <div>
            <img src="guitarra-eletrica.png">
            <h1>Lista de Músicas</h1>
        </div>
        <p>Adicione suas músicas, álbuns e artistas/bandas favoritos</p>
    </header>
    <main>
        <section id="list1">
            <h2>Músicas</h2>
            <form id="form1">
                <input type="text" id="item1" placeholder="Adicionar música" required>
                <textarea id="description1" placeholder="Adicionar descrição" required></textarea>
                <input type="file" id="image1" accept="image/*" required>
                <button type="submit">Adicionar</button>
            </form>
            <ul id="items1"></ul>
        </section>
        <section id="list2">
            <h2>Álbuns</h2>
            <form id="form2">
                <input type="text" id="item2" placeholder="Adicionar álbum" required>
                <textarea id="description2" placeholder="Adicionar descrição" required></textarea>
                <input type="file" id="image2" accept="image/*" required>
                <button type="submit">Adicionar</button>
            </form>
            <ul id="items2"></ul>
        </section>
        <section id="list3">
            <h2>Artistas/Bandas</h2>
            <form id="form3">
                <input type="text" id="item3" placeholder="Adicionar artista/banda" required>
                <textarea id="description3" placeholder="Adicionar descrição" required></textarea>
                <input type="file" id="image3" accept="image/*" required>
                <button type="submit">Adicionar</button>
            </form>
            <ul id="items3"></ul>
        </section>
    </main>
    <script>
        document.addEventListener('DOMContentLoaded', () => {
            function addItem(listId, inputId, fileId, descId) {
                const list = document.getElementById(listId);
                const input = document.getElementById(inputId);
                const fileInput = document.getElementById(fileId);
                const descInput = document.getElementById(descId);
                const itemText = input.value;
                const description = descInput.value;
                const file = fileInput.files[0];

                if (itemText && file && description) {
                    const listItem = document.createElement('li');
                    
                    const itemHeader = document.createElement('div');
                    itemHeader.className = 'item-header';

                    const span = document.createElement('span');
                    span.textContent = itemText;

                    const indicator = document.createElement('span');
                    indicator.textContent = '˅';
                    indicator.style.fontSize = '1em';

                    itemHeader.appendChild(span);
                    itemHeader.appendChild(indicator);
                    
                    const itemDetails = document.createElement('div');
                    itemDetails.className = 'item-details';

                    const img = document.createElement('img');
                    const reader = new FileReader();
                    reader.onload = (e) => {
                        img.src = e.target.result;
                    };
                    reader.readAsDataURL(file);

                    const descParagraph = document.createElement('p');
                    descParagraph.textContent = description;

                    const button = document.createElement('button');
                    button.textContent = 'Excluir';
                    button.addEventListener('click', (e) => {
                        e.stopPropagation();
                        list.removeChild(listItem);
                    });

                    itemDetails.appendChild(img);
                    itemDetails.appendChild(descParagraph);
                    itemDetails.appendChild(button);

                    listItem.appendChild(itemHeader);
                    listItem.appendChild(itemDetails);
                    list.appendChild(listItem);

                    listItem.addEventListener('click', () => {
                        itemDetails.style.display = itemDetails.style.display === 'none' ? 'flex' : 'none';
                    });

                    input.value = '';
                    fileInput.value = '';
                    descInput.value = '';
                }
            }

            document.getElementById('form1').addEventListener('submit', (e) => {
                e.preventDefault();
                addItem('items1', 'item1', 'image1', 'description1');
            });

            document.getElementById('form2').addEventListener('submit', (e) => {
                e.preventDefault();
                addItem('items2', 'item2', 'image2', 'description2');
            });

            document.getElementById('form3').addEventListener('submit', (e) => {
                e.preventDefault();
                addItem('items3', 'item3', 'image3', 'description3');
            });
        });
    </script>
</body>
</html>
