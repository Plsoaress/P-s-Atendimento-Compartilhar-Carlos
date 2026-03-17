//P-s-Atendimento-Compartilhar-Carlos--/

<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <title>Texto para CSV</title>
</head>
<body>
 
<h2>Converter Texto em CSV</h2>
<p>Segurado;Telefone;Matricula;Agente;Cia;Servico;Placa</p>
 
<textarea id="textoInput" rows="12" cols="100"
placeholder="Segurado;Telefone;Matricula;Agente;Cia;Servico;Placa"></textarea>
 
<br><br>
 
<button onclick="gerarCSV()">Gerar CSV</button>
 
<script>
function gerarCSV() {
    const texto = document.getElementById("textoInput").value.trim();
    if (!texto) {
        alert("Cole algum texto.");
        return;
    }
 
    const linhas = texto.split(/\r?\n/);
 
    const colunas = [
        "Segurado",
        "Telefone",
        "Matricula",
        "Agente",
        "Cia",
        "Servico",
        "Placa"
    ];
 
    let csv = colunas.join(",") + "\n";
 
    linhas.forEach(linha => {
        if (!linha.trim()) return;
 
        const campos = linha.split(/[;,\|\t]/);
 
        const registro = [];
        for (let i = 0; i < colunas.length; i++) {
            registro.push(campos[i] ? campos[i].trim() : "");
        }
 
        // SEM ASPAS
        csv += registro.join(",") + "\n";
    });
 
    const blob = new Blob([csv], { type: "text/csv;charset=utf-8;" });
    const link = document.createElement("a");
    link.href = URL.createObjectURL(blob);
    link.download = "dados.csv";
    link.click();
}
</script>
 
</body>
</html>
