# newtonshmkdir newtonshop
cd newtonshop
op.onrender.com
npx create-react-app frontend
cd frontend
import React, { useState, useEffect } from 'react';
import axios from 'axios';
import './App.css';

const App = () => {
  const [produtos, setProdutos] = useState([]);

  useEffect(() => {
    axios.get("https://localhost:5000/produtos")  // A URL do seu backend
      .then(response => setProdutos(response.data))
      .catch(err => console.log(err));
  }, []);

  return (
    <div className="App">
      <h1>Newton Shop - Loja de Tecnologia</h1>
      <div className="produtos">
        {produtos.map(produto => (
          <div key={produto.id} className="produto">
            <img src={produto.imagem} alt={produto.nome} />
            <h2>{produto.nome}</h2>
            <p>{produto.preco}</p>
            <button>Comprar</button>
          </div>
        ))}
      </div>
    </div>
  );
}

export default App;
mkdir backend
cd backend
const express = require('express');
const cors = require('cors');
const app = express();

// Dados fictícios de produtos (podem ser extraídos de um banco de dados mais tarde)
const produtos = [
  { id: 1, nome: 'Smartphone', preco: 'R$ 1500,00', imagem: 'https://via.placeholder.com/200' },
  { id: 2, nome: 'Notebook', preco: 'R$ 4000,00', imagem: 'https://via.placeholder.com/200' },
];

// Habilitando CORS para permitir requisições do frontend
app.use(cors());

// Endpoint para listar os produtos
app.get('/produtos', (req, res) => {
  res.json(produtos);
});

// Iniciando o servidor na porta 5000
const PORT = process.env.PORT || 5000;
app.listen(PORT, () => {
  console.log(`Servidor rodando em http://localhost:${PORT}`);
});
npm init -y
npm install express cors
npm start
