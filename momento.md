


<h3>1- Quantos funcionários da empresa Momento trabalham no departamento de vendas?</h3>
<b>Resposta:</b> 10 funcionários.

<pre>
db.funcionarios.countDocuments({departamento: ObjectId('85992103f9b3e0b3b3c1fe71')})
</pre>

---

<h3>2- Inclua suas próprias informações no departamento de Tecnologia da empresa.</h3>

<pre>
db.funcionarios.insertOne({
  nome: 'Murilo Coelho',
  telefone: '11.97792.3128',
  email: 'coelho.murilo10@gmail.com',
  dataAdmissao: '2024-09-24',
  cargo: 'Full-Stack Developer',
  salario: 15000,
  departamento: ObjectId('85992103f9b3e0b3b3c1fe74')
})
</pre>

---

<h3>3- Quantos funcionários temos ao total na empresa?</h3>
<b>Resposta:</b> 24 funcionários.

<pre>
db.funcionarios.countDocuments()
</pre>

---

<h3>4- E quanto ao Departamento de Tecnologia?</h3>
<b>Resposta:</b> 5 funcionários.

<pre>
db.funcionarios.countDocuments({departamento: ObjectId('85992103f9b3e0b3b3c1fe74')})
</pre>

---

<h3>5- Qual a média salarial do departamento de tecnologia?</h3>
<b>Resposta:</b> 6.300.

<pre>
db.funcionarios.aggregate([
  {
    $match: {departamento: ObjectId('85992103f9b3e0b3b3c1fe74')}
  },
  {
    $group: {
      _id: null,
      totalsalario: {$sum: "$salario"},
      totalfun: {$sum: 1}
    }
  },
  {
    $project: {
      _id: 0,
      mediasalarios: {$divide: ["$totalsalario", "$totalfun"]}
    }
  }
])
</pre>

---

<h3>6- Quanto o departamento de Vendas gasta em salários?</h3>
<b>Resposta:</b> 95.100.

<pre>
db.funcionarios.aggregate([
  {
    $match: {departamento: ObjectId('85992103f9b3e0b3b3c1fe71')}
  },
  {
    $group: {
      _id: 0,
      somasalario: {$sum: '$salario'}
    }
  }
])
</pre>

---

<h3>7- Um novo departamento foi criado. O departamento de Inovações. Ele será locado no Brasil. Por favor, adicione-o no banco de dados da empresa colocando quaisquer informações que você achar relevantes.</h3>

<pre>
db.escritorios.insertOne({
  id: ObjectId('66f55f759d35357448a2f50d'),
  nome: 'Wakanda Offices',
  endereco: 'Black Panther Enterprises, 1008 Jaraguá, Wakanda, 015-5047',
  telefone: '11.948.458.2489',
  pais: 'Brasil',
  suprimentos: [
    {
      produto: 'Cafeteiras',
      quantidade: 7,
      precoUnitario: 283.75
    },
    {
      produto: 'Kit de Papel A4',
      quantidade: 50,
      precoUnitario: 752.85
    },
    {
      produto: 'Playstation 5',
      quantidade: 2,
      precoUnitario: 7400.80
    },
    {
      produto: 'Post-its',
      quantidade: 50,
      precoUnitario: 1000
    },
    {
      produto: 'PC gamer',
      quantidade: 10,
      precoUnitario: 25000
    }
  ]
})

db.departamentos.insertOne({
  nome: 'inovações',
  escritorio: ObjectId()
})
</pre>






<h3>8- O departamento de Inovações está sem funcionários. Inclua alguns colegas de turma nesse departamento.</h3>

<pre>
db.funcionarios.insertMany([
  {
    nome: 'Victor Curtis',
    telefone: '11-00000.0000',
    email: 'v.c@123.com',
    dataAdmissao: '2010-02-05',
    salario: 1100,
    cargo: 'Full-Stack Developer',
    departamento: ObjectId('66f55f759d35357448a2f50e')
  },
  {
    nome: 'Andressa Prudente',
    telefone: '11-22222.1111',
    email: 'A.P@123.com',
    dataAdmissao: '2021-09-24',
    cargo: 'Scrum Master',
    salario: 15000,
    departamento: ObjectId('66f55f759d35357448a2f50e')
  },
  {
    nome: 'Ana Cristina',
    telefone: '11-11111.2222',
    email: 'A.C@123.com',
    dataAdmissao: '2022-09-24',
    cargo: 'Full-Stack Developer',
    salario: 10000,
    departamento: ObjectId('66f55f759d35357448a2f50e')
  }
])
</pre>

---

<h3>9- Quantos funcionários a empresa Momento tem agora?</h3>
<b>Resposta:</b> 27 funcionários.

<pre>
db.funcionarios.countDocuments()
</pre>

---

<h3>10- Quantos funcionários da empresa Momento possuem cônjuges?</h3>
<b>Resposta:</b> 7 funcionários.

<pre>
db.funcionarios.countDocuments({"dependentes.conjuge": {$exists: true}})
</pre>

---

<h3>11- Qual a média salarial dos funcionários da empresa Momento, excluindo-se o CEO?</h3>
<b>Resposta:</b> 9.837,69.

<pre>
db.funcionarios.aggregate([
  {
    $match: {cargo: {$ne: "CEO"}}
  },
  {
    $group: {
      _id: null,
      somasal: {$sum: "$salario"},
      somafun: {$sum: 1}
    }
  },
  {
    $project: {
      _id: 0,
      mediasal: {$divide: ['$somasal', '$somafun']}
    }
  }
])
</pre>

---

<h3>12- Qual a média salarial do departamento de Tecnologia?</h3>
<b>Resposta:</b> 6.300.

<pre>
db.funcionarios.aggregate([
  {
    $match: {departamento: ObjectId('85992103f9b3e0b3b3c1fe74')}
  },
  {
    $group: {
      _id: null,
      somasal: {$sum: "$salario"},
      somafun: {$sum: 1}
    }
  },
  {
    $project: {
      _id: 0,
      mediasal: {$divide: ['$somasal', '$somafun']}
    }
  }
])
</pre>

---

<h3>13- Qual o departamento com a maior média salarial?</h3>
<b>Resposta:</b> Executivo, com média de 71.000.

<pre>
db.funcionarios.aggregate([
  {
    $group: {
      _id: "$departamento",
      somasal: {$sum: "$salario"},
      somafun: {$sum: 1}
    }
  },
  {
    $project: {
      departamento: "$_id",
      _id: "$departamento",
      mediasal: {$divide: ['$somasal', '$somafun']}
    }
  },
  {
    $sort: {"mediasal": -1}
  },
  {
    $limit: 1
  }
])
</pre>

---

<h3>14- Qual o departamento com o menor número de funcionários?</h3>
<b>Resposta:</b> Executivo, com apenas 1 funcionário.

<pre>
db.funcionarios.aggregate([
  {
    $group: {
      _id: "$departamento",
      somafun: {$sum: 1}
    }
  },
  {
    $sort: {"somafun": 1}
  },
  {
    $limit: 1
  }
])
</pre>

---

<h3>15- Pensando na relação quantidade e valor unitário, qual o produto mais valioso da empresa?</h3>
<b>Resposta:</b> Sabre de luz.

<pre>
db.vendas.aggregate([
  {
    $sort: {quantidade: -1}
  },
  {
    $sort: {precoUnitario: -1}
  },
  {
    $limit: 1
  }
])
</pre>

---

<h3>16- Qual o produto mais vendido da empresa?</h3>
<b>Resposta:</b> Uniforme de Moléculas Instáveis.

<pre>
db.vendas.aggregate([
  {
    $sort: {quantidade: -1}
  },
  {
    $limit: 1
  }
])
</pre>

---

<h3>17- Qual o produto menos vendido da empresa?</h3>
<b>Resposta:</b> Uniforme do Superman.

<pre>
db.vendas.aggregate([
  {
    $sort: {quantidade: 1}
  },
  {
    $limit: 1
  }
])
</pre>

---

<h3>18- Qual o total gasto em suprimentos no escritório Wakanda Offices?</h3>
<b>Resposta:</b> Total gasto em suprimentos.

<pre>
db.escritorios.aggregate([
  {
    $match: {nome: 'Wakanda Offices'}
  },
  {
    $unwind: "$suprimentos"
  },
  {
    $group: {
      _id: null,
      totalGasto: {$sum: {$multiply: ["$suprimentos.quantidade", "$suprimentos.precoUnitario"]}}
    }
  }
])
</pre>

---

Essas queries devem cobrir até a questão 18.


