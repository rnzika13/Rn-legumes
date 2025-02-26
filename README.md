<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>RN LEGUMES</title>
    <style>
        body { 
            font-family: Arial, sans-serif; 
            text-align: center; 
            font-size: 1em; 
            background-color: #ffffff;
        }
        .container { 
            max-width: 600px; 
            margin: auto; 
            background: rgba(255, 255, 255, 0.8); 
            padding: 20px; 
            border-radius: 10px; 
        }
        .item { 
            display: flex; 
            justify-content: space-between; 
            margin: 5px 0; 
            font-size: 0.85em; 
            font-weight: bold;
        }
        .item input { width: 50px; margin-left: 10px; }
        button { margin-top: 20px; padding: 10px; font-size: 1em; }
    </style>
</head>
<body>
    <div class="container">
        <h2>Escolha os itens</h2>
        <h3>Verduras</h3>
        <h4>Folhosas</h4>
        <div id="folhosas"></div>
        <h4>Temperos</h4>
        <div id="temperos"></div>
        <h3>Legumes</h3>
        <h4>Raízes e tubérculos</h4>
        <div id="raizes"></div>
        <h4>Frutos</h4>
        <div id="frutos"></div>
        <h3>Cogumelos</h3>
        <div id="cogumelos"></div>
        <button onclick="enviarWhatsApp()">Enviar para WhatsApp</button>
    </div>

    <script>
        const folhosas = [
            "Alface crespa", "Alface lisa", "Alface americana", "Alface mista (s/ cenoura)", "Agrião",
            "Escarola", "Almeirão", "Espinafre pic.", "Couve", "Repolho", "Repolho roxo", "Acelga c/ cen."
        ];
        
        const temperos = [
            "Salsinha", "Cebolinha", "Salsinha/cebolinha", "Alho-poró"
        ];

        const raizes = [
            "Cenoura", "Beterraba", "Mandioquinha", "Inhame", "Batata-doce", "Batata-doce roxa",
            "Batata-doce jap.", "Cará", "Mandioca crua", "Mandioca coz.", "Gengibre", "Açafrão"
        ];
        
        const frutos = [
            "Berinjela", "Berinjela jap.", "Chuchu", "Pepino jap.", "Pepino caipira", "Jiló", "Quiabo",
            "Abobrinha bras.", "Abobrinha ital.", "Pimentões (3 cores)", "Milho doce", "Milho verde trad.",
            "Abób. cabotiá pic./fatiada", "Abób. p/ doce", "Pimenta d.-de-moça", "Pimenta de cheiro"
        ];
        
        const cogumelos = [
            "Shimeji preto", "Shiitake", "Porto Belo", "Paris"
        ];
        
        function adicionarItens(lista, divId) {
            const listaDiv = document.getElementById(divId);
            lista.forEach(item => {
                const div = document.createElement("div");
                div.classList.add("item");
                div.innerHTML = `
                    <label>
                        <input type='checkbox' value='${item}'> ${item}
                    </label>
                    <input type='number' min='1' placeholder='Qtd' class='quantidade'>
                    <select class='unidade'>
                        <option value='kg'>Kg</option>
                        <option value='un'>Unidade</option>
                        <option value='pacote'>Pacote</option>
                    </select>
                `;
                listaDiv.appendChild(div);
            });
        }

        adicionarItens(folhosas, "folhosas");
        adicionarItens(temperos, "temperos");
        adicionarItens(raizes, "raizes");
        adicionarItens(frutos, "frutos");
        adicionarItens(cogumelos, "cogumelos");
        
        function enviarWhatsApp() {
            let selecionados = [];
            document.querySelectorAll(".item").forEach(div => {
                let checkbox = div.querySelector("input[type=checkbox]");
                let quantidade = div.querySelector(".quantidade").value;
                let unidade = div.querySelector(".unidade").value;
                
                if (checkbox.checked && quantidade) {
                    selecionados.push(`${quantidade} ${unidade} de ${checkbox.value}`);
                }
            });
            
            if (selecionados.length === 0) {
                alert("Selecione pelo menos um item e informe a quantidade!");
                return;
            }
            
            let mensagem = "Olá, gostaria de pedir:\n" + selecionados.join("\n");
            let numero = "5511942653446"; // Altere para seu número com DDD e código do país
            let link = `https://wa.me/${numero}?text=${encodeURIComponent(mensagem)}`;
            window.open(link, "_blank");
        }
    </script>
</body>
</html>
