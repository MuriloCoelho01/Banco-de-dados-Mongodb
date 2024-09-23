<h1>Atividades de Banco de Dados - MongoDB</h1>

<p>Atividade visa desenvolver nossa capacidade de manipulação de <b>Banco de Dados</b> <br>
utilizando o a Metodologia <b>CRUD</b><br><br>
<b>C - Create<br>
R - Read <br>
U - Update <br>
D - Delete <br>
</p>
<hr>
<h3>Exercícios</h3>

<h4>1- Quantas vezes Natalie Portman foi indicada ao Oscar?</h4>
<p>Natalie Portman foi indicada 3 vezes ao Oscar.</p>

<h4>Query:</h4>
<pre>db.registros.countDocuments({nome_do_indicado: "Natalie Portman"})</pre>

<br><br>

<h4>2- Quantos Oscars Natalie Portman ganhou?</h4>
<p>Natalie Portman ganhou 1 Oscar.</p>

<h4>Query:</h4>
<pre>db.registros.countDocuments({nome_do_indicado: "Natalie Portman", vencedor: "true"})</pre>

<br><br>

<h4>3- Amy Adams já ganhou algum Oscar?</h4>
<p>Não, Amy Adams não ganhou nenhum Oscar.</p>

<h4>Query:</h4>
<pre>db.registros.countDocuments({nome_do_indicado: "Amy Adams", vencedor: "true"})</pre>

<br><br>

<h4>4- A série de filmes Toy Story ganhou um Oscar em quais anos?</h4>
<p>Toy Story 3 ganhou 2 prêmios em 2011 e Toy Story 4 ganhou 1 prêmio em 2020.</p>

<h4>Query:</h4>
<pre>db.registros.find({nome_do_filme: /toy story/i, vencedor: "true"})</pre>

<br><br>

<h4>5- A partir de que ano a categoria "Actress" deixa de existir?</h4>
<p>A partir de 1976.</p>

<h4>Query:</h4>
<pre>db.registros.find({categoria: "ACTRESS"}).sort({cerimonia: -1})</pre>

<br><br>

<h4>6- O primeiro Oscar para melhor Atriz foi para quem? Em que ano?</h4>
<p>Foi para Janet Gaynor, em 1928.</p>

<h4>Query:</h4>
<pre>db.registros.find({categoria: "ACTRESS", vencedor: "true"}).sort({cerimonia: 1})</pre>

<br><br>

<h4>7- No campo "Vencedor", altere todos os valores "true" para 1 e todos os valores "false" para 0.</h4>

<h4>Query para alterar "true" para 1:</h4>
<pre>db.registros.updateMany({vencedor: "true"}, {$set: {vencedor: "1"}})</pre>

<h4>Query para alterar "false" para 0:</h4>
<pre>db.registros.updateMany({vencedor: "false"}, {$set: {vencedor: "0"}})</pre>

<br><br>

<h4>8- Em qual edição do Oscar "Crash" concorreu ao Oscar?</h4>
<p>O filme "Crash" concorreu ao Oscar em 2006.</p>

<h4>Query:</h4>
<pre>db.registros.find({nome_do_filme: "Crash"})</pre>

<br><br>

<h4>9- Dê um Oscar para um filme que merece muito, mas não ganhou.</h4>
<p>Dei um Oscar para o filme "Carros".</p>

<h4>Query:</h4>
<pre>db.registros.updateOne({nome_do_filme: "Cars"}, {$set: {vencedor: "1"}})</pre>

<br><br>

<h4>10- O filme "Central do Brasil" aparece no Oscar?</h4>
<p>Sim, no ano de 1999.</p>

<h4>Query:</h4>
<pre>db.registros.find({nome_do_filme: "Central Station"})</pre>

<br><br>

<h4>11- Inclua no banco 3 filmes que nunca foram nomeados ao Oscar, mas que merecem ser.</h4>

<h4>Query:</h4>
<pre>db.registros.insertMany([
{
 'id_registro': 107507,
 'ano_filmagem': 2001,
 'ano_cerimonia': 2002,
 'cerimonia': 74,
 'categoria': 'BEST PICTURE 2',
 'nome_do_indicado': 'Jesse Dylan, Producer',
 'nome_do_filme': 'How High',
 'vencedor': '1'
},
{
 'id_registro': 107608,
 'ano_filmagem': 2000,
 'ano_cerimonia': 2001,
 'cerimonia': 79,
 'categoria': 'BEST PICTURE 2',
 'nome_do_indicado': 'Keenen Ivory Wayans, Producer',
 'nome_do_filme': 'Scary Movie',
 'vencedor': '1'
},
{
 'id_registro': 1097010,
 'ano_filmagem': 2001,
 'ano_cerimonia': 2002,
 'cerimonia': 80,
 'categoria': 'BEST PICTURE 2',
 'nome_do_indicado': 'Keenen Ivory Wayans, Producer',
 'nome_do_filme': 'Scary Movie 2',
 'vencedor': '1'
}
])</pre>

<br><br>

<h4>12- Pensando no ano em que você nasceu: Qual foi o Oscar de Melhor Filme, Melhor Atriz e Melhor Diretor?</h4>
<p>Melhor Filme: "Crash".</p>
<p>Melhor Atriz: Reese Witherspoon.</p>
<p>Melhor Diretor: Ang Lee.</p>

<h4>Query Melhor Filme:</h4>
<pre>db.registros.find({ano_cerimonia: 2006, categoria: /best/i, vencedor: "1"})</pre>

<h4>Query Melhor Atriz:</h4>
<pre>db.registros.find({ano_cerimonia: 2006, categoria: /Actress/i, vencedor: "1"})</pre>

<h4>Query Melhor Diretor:</h4>
<pre>db.registros.find({ano_cerimonia: 2006, categoria: "DIRECTING", vencedor: "1"})</pre>
