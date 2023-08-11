# Projeto Copa Feminina 2023 em React JS com Vite

## Aula 02 Criar Component GameTable

> Vamos criar o component GameTable para exibir a tabela de jogos

## Criar component GameTable

1. Dentro da pasta `src` crie a pasta `components`
2. Dentro da pasta `components` crie a pasta `GameTable`
3. Dentro da pasta `GameTable` crie os 2 arquivos 'index.jsx' e 'Card.module.css'
4. Abra o arquivo `index.jsx`
5. Deixe o código da seguinte forma:

~~~javascript
import { useState } from 'react'
import styles from './GameTable.module.css'
import { useEffect } from 'react'

function GameTable() {
    
    const [ jogos, setJogos ] = useState([])

    useEffect(() => {
        const buscarJogos = async () => {
            const response = await fetch('https://raw.githubusercontent.com/edsonmaia/apifakecopa2023/main/tabela-copa-feminina-2023.json')
            const data = await response.json()
            setJogos(data)
        }
        buscarJogos()
    }, [])
    
    return (
        <table className={styles.table}>
            <thead>
                <tr>
                    <th>Dia</th>
                    <th>Data</th>
                    <th>Hora</th>
                    <th>Grupo</th>
                    <th colSpan={5}>Jogo</th>
                </tr>
            </thead>
            <tbody>
                {
                    jogos.map( jogo => (
                        <tr key={jogo.jogo}>
                            <td>{jogo.dia}</td>
                            <td>{jogo.data}</td>
                            <td>{jogo.hora}</td>
                            <td>{jogo.grupo}</td>
                            <td>
                                <span className={styles.direita}>
                                    {jogo.mandante}
                                    <img src={`/bandeiras/${jogo.sigla_mandante.toLowerCase()}.png`} alt={jogo.mandante} />
                                </span>
                            </td>
                            <td className={styles.gols}>{jogo.gols_mandante}</td>
                            <td>X</td>
                            <td className={styles.gols}>{jogo.gols_visitante}</td>
                            <td>
                                <span className={styles.esquerda}>
                                    <img src={`/bandeiras/${jogo.sigla_visitante.toLowerCase()}.png`} alt={jogo.visitante} />
                                    {jogo.visitante}
                                </span>
                            </td>
                        </tr>
                    ))
                }
            </tbody>
        </table>
    )
}

export default GameTable

~~~

6. Salve as alterações.

## Como usar o component GameTable

1. Abra o arquivo `App.jsx`
2. Abaixo da section cards adicione uma tag h2, uma section e dentro dela o componente GameTable. Deixe o código da seguinte forma:

~~~javascript
import './App.css'
import Card from './components/Card'
import GameTable from './components/GameTable'

function App() {

  return (
    <>
      <h1>Copa do Mundo Feminina 2023</h1>
      <section className='cards'>
        <Card />
      </section>

      <h2>Tabela de Jogos</h2>

      <section className='game_table'>
        <GameTable />
      </section>
    </>
  )
}

export default App

~~~

3. Faça o import do component GameTable

~~~javascript
import Card from './components/GameTable'
~~~

4. Salve as alterações e veja o Resultado no browser.

## CSS do component GameTable

1. Abra o arquivo GameTable.module.css
2. Faça o seguinte código:

~~~css
.table {
    width: 100%;
    max-width: 1000px;
    margin-block: 1rem;
    margin-inline: auto;
    border-collapse: collapse;
    
}

.table tr {
    height: 50px;
    border-bottom: 1px solid #ccc;
}

.table tr:nth-child(even) {
    background-color: #f2f2f2;
}

.table td {
    text-align: center;
}

.table th {
    background-color: #f2f2f2;
    height: 50px;
    border-bottom: 1px solid #ccc;
    position: sticky;
    top: 0;
}

.esquerda {
    display: flex;
    align-items: center;
    justify-content: start;
    gap: 0.5rem;
}

.direita {
    display: flex;
    align-items: center;
    justify-content: end;
    gap: 0.5rem;
}

.gols {
    font-size: 2rem;
}

~~~

3. Salve as alterações e veja o resultado no browser.

> Vimos nesta aula como criar o componente GameTable para exibir as informações uma tabela de jogos. Revimos como fazer uso de useState e useEffect, fazer requisição assíncrona para obter os dados para criar as linhas da tabela com os 48 jogos da primeira fase dinamicamente.
> Na próxima aula vamos ver como criar novas funcionalidades e fazer ajustes no nosso projeto.

Salve Devs até a próxima!
