# Projeto Copa Feminina 2023 em React JS com Vite

## Aula 03 Criar Component GroupStandings

> Vamos criar o component ## Aula 03 Criar Component GroupStandings
 para exibir a tabela com a classificação por grupo

## Criar component GroupStandings

1. Dentro da pasta `src` crie a pasta `components`
2. Dentro da pasta `components` crie a pasta `GroupStandings`
3. Dentro da pasta `GroupStandings` crie os 2 arquivos 'index.jsx' e 'GroupStandings.module.css'
4. Abra o arquivo `index.jsx`
5. Deixe o código da seguinte forma:

~~~jsx
import { useEffect, useState } from 'react'
import styles from './GroupStandings.module.css'

function GroupStandings() {

    const [ grupos, setGrupos ] = useState([])

    useEffect(() => {
        const buscarGrupos = async () => {
            const response = await fetch('https://raw.githubusercontent.com/edsonmaia/apifakecopa2023/main/classificacao-por-grupos-2023.json')
            const data = await response.json()
            setGrupos(data)
        }
        buscarGrupos()
    }, [])

    return (
        <section>
            <h2>Grupo A</h2>
            <table className={styles.table}>
                <thead>
                    <tr>
                        <th>#</th>
                        <th>Seleção</th>
                        <th>Pontos</th>
                        <th>Vitórias</th>
                        <th>Empates</th>
                        <th>Derrotas</th>
                        <th>Gols Pró</th>
                        <th>Gols Contra</th>
                        <th>Saldo de Gols</th>
                    </tr>
                </thead>
                <tbody>
                    {
                        grupos.filter( grupo => grupo.grupo === "A" )
                        .map( grupo => (
                            <tr key={grupo.selecao}>
                                <td>{grupo.posicao}</td>
                                <td className={styles.esquerda}>{grupo.selecao}</td>
                                <td>{grupo.pontos}</td>
                                <td>{grupo.vitorias}</td>
                                <td>{grupo.empates}</td>
                                <td>{grupo.derrotas}</td>
                                <td>{grupo.gols_pro}</td>
                                <td>{grupo.gols_contra}</td>
                                <td>{grupo.saldo_gols}</td>
                            </tr>
                        ))
                    }
                </tbody>
            </table>
        </section>
        
    )
}

export default GroupStandings

~~~

## Como usar o componente GroupStandings

1. Abra o arquivo `App.jsx`
2. Abaixo da section game_table deixe o código da seguinte forma:

~~~jsx
import './App.css'
import Card from './components/Card'
import GameTable from './components/GameTable'
import GroupStandings from './components/GroupStangings'

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

      <h2>Classificação dos Grupos</h2>

      <section className='group_standings'>
      	<h2>Grupo A</h2>
        <GroupStandings />
      </section>

    </>

  )
}

export default App

~~~

3. Salve as alterações e veja o resultado no browser.

## CSS de GroupStandings

1. Abra o arquivo GroupStandings.module.css
2. Faça o seguinte código:

~~~css
.table {
    width: 100%;
    max-width: 1000px;
    border-collapse: collapse;
    margin: 1rem auto;
}

.table tr {
    border-bottom: 1px solid #ccc;
    height: 50px;
}

.table tr:nth-child(even) {
    background-color: #f2f2f2;
}

.table th {
    background-color: #f2f2f2;
    position: sticky;
    top: 0;
}

table .esquerda {
    text-align: left;
    padding-left: 1rem;
}

~~~

3. Salve as alterações e veja o resultado no browser.

> Vimos nesta aula como criar o componente GroupStandings para exibir as informações uma tabela de classifição por grupos. Revimos como fazer uso de useState e useEffect, fazer requisição assíncrona para obter os dados para criar as linhas da tabela dinamicamente.
> Vimos também como trabalhar com filter do map.
> Na próxima aula vamos ver como criar novas funcionalidades e fazer ajustes no nosso projeto para filtrar dinamicamente a exibição dos grupos após escolhermos a letra do grupo em uma caixa de seleção.

Salve Devs até a próxima!
