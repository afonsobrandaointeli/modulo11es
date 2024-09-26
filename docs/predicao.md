# Processamento e Predição em Produção (Resumão do módulo!)

## Autoestudos

|Autestudo|Descrição|Link|
|---------|---------|----|
|Previsões através de API Endpoint com FastAPI|Este autoestudo ensina como conectar os modelos preditivos em uma API de endpoints e previsão.|[Link](https://imasters.com.br/back-end/padroes-de-web-api-parte-02-middleware)|

<hr>
<div style="display: flex; justify-content: center; align-items: center;">
    <div class="carde">
        <img src="https://instructionaldev.umassd.edu/files/2023/05/kahoot-logo.jpg" alt="Imagem do Card">
        <div class="card-bodye">
            <a href="https://kahoot.it" class="btn">Vamos!</a>
        </div>
    </div>
</div>

---

# Entregas da Semana

<table>
    <thead>
        <tr>
            <th>Artefato</th>
            <th>Descrição</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Implantação do Pipeline na Nuvem</td>
            <td><span class="clickable" onclick="showCard('card1')">Descrição</span></td>
        </tr>
        <tr>
            <td>Acesso, LGPD e Governança de Dados</td>
            <td><span class="clickable" onclick="showCard('card2')">Descrição</span></td>
        </tr>
        <tr>
            <td>Dashboard (1ª versão)</td>
            <td><span class="clickable" onclick="showCard('card3')">Descrição</span></td>
        </tr>
    </tbody>
</table>

<div id="card1" class="card">
    <h3>Implantação do Pipeline na Nuvem</h3>
    <p>A implantação de um pipeline de dados é um processo crítico que envolve a configuração e o gerenciamento de um sistema automatizado para a coleta, transformação e transporte de dados de uma fonte para um destino desejado. Esse artefato é fundamental para garantir a eficiência na ingestão, processamento e armazenamento de informações, permitindo que as organizações ajam com base em dados em tempo real ou com baixa latência. Durante a implantação do pipeline, é importante configurar os fluxos de dados, implementar a lógica de transformação, definir estratégias de monitoramento e gerenciamento e garantir a segurança e a qualidade dos dados. Essa implementação é crucial para as operações de uma empresa, oferecendo insights acionáveis e informações precisas para orientar decisões informadas.</p>
</div>

<div id="card2" class="card">
    <h3>Acesso, LGPD e Governança de Dados</h3>
    <p>A "Documentação de Acesso, LGPD e Governança de Dados" assume um papel fundamental na gestão eficaz dos dados em conformidade com a Lei Geral de Proteção de Dados (LGPD) e nos processos de governança. Essa documentação não apenas delineia as políticas e procedimentos de acesso aos dados, mas também estabelece as salvaguardas necessárias para proteger a privacidade e a segurança das informações. Ao integrar aspectos da LGPD, a documentação assegura que os dados sejam manuseados de maneira ética, legal e transparente, contribuindo para a construção de uma cultura organizacional comprometida com a privacidade. Além disso, a ênfase na governança de dados garante a qualidade e a integridade dos dados ao longo do tempo, promovendo uma tomada de decisões mais informada e alinhada aos objetivos estratégicos da organização. Essa abordagem abrangente na documentação reflete um comprometimento com a conformidade legal, ética e a excelência na gestão de dados.</p>
</div>

<div id="card3" class="card">
    <h3>Dashboard (1ª versão)</h3>
    <p>Neste artefato, o grupo deve produzir uma versão preliminar de Dashboard, de acordo com o serviço ou ferramenta escolhida (ex. Streamlit) em conformidade com o wireframe anterior. Esta versão preliminar deve ser implementada já na ferramenta ou serviço escolhido. O objetivo deste artefato é estabelecer um primeiro estudo da interface de governança de dados, que permita ao grupo realizar testes de usabilidade a partir de tarefas relacionadas ao uso de gráficos/tabelas interativos. Assim, o grupo também deve produzir um plano de tarefas possíveis de serem realizadas sobre o protótipo/implementação da Dashboard, com enunciados alinhados às necessidades do usuário da interface de governança de dados. O formato deste plano pode ser publicado como documento markdown no repositório github, e cada enunciado de tarefa pode seguir o formato "Suponha que (contexto), use a dashboard para (necessidade do usuário)".</p>
</div>

# -> Vamos focar nos artefatos!

<script>
    function showCard(cardId) {
        // Esconde todos os cards
        const cards = document.querySelectorAll('.card');
        cards.forEach(card => card.classList.remove('active'));

        // Mostra o card correspondente
        const card = document.getElementById(cardId);
        if (card) {
            card.classList.add('active');
        }
    }
</script>

<style>
    .carde {
        width: 300px;
        border-radius: 10px;
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        overflow: hidden;
        background-color: #fff;
        text-align: center;
    }

    .carde img {
        width: 100%;
        height: auto;
    }

    .card-bodye {
        padding: 20px;
    }

    .card-title {
        font-size: 1.5rem;
        margin-bottom: 15px;
    }

    .card-text {
        font-size: 1rem;
        margin-bottom: 20px;
        color: #666;
    }
    .btn {
        display: inline-block;
        padding: 10px 20px;
        background-color: #007bff;
        color: white;
        text-decoration: none;
        border-radius: 5px;
        transition: background-color 0.3s ease;
    }
    .btn:hover {
        background-color: #0056b3;
    }
    
    table {
        width: 100%;
        border-collapse: collapse;
        margin-bottom: 20px;
    }

    table, th, td {
        border: 1px solid black;
    }

    th, td {
        padding: 10px;
        text-align: left;
    }

    .card {
        display: none;
        border: 1px solid #ccc;
        padding: 20px;
        border-radius: 5px;
        margin-top: 10px;
        background-color: #f9f9f9;
    }

    .card.active {
        display: block;
    }

    .clickable {
        display: inline-block;
        font-weight: bold;
        padding: 5px 10px;
        background-color: #d3d3d3; /* Cinza claro */
        color: #000;
        border: 1px solid #aaa; /* Cinza para o contorno */
        border-radius: 5px;
        cursor: pointer;
        text-decoration: none;
        transition: background-color 0.3s ease;
    }

    .clickable:hover {
        background-color: #bbb; /* Cinza mais escuro no hover */
    }
</style>