# Projeto Copa Feminina 2023 em React JS com Vite

## Aula 04 Refatorar Component GroupStandings

> Vamos refatorar o component GroupStandings para exibir uma caixa de seleção que será usada como critério para a tabela com a classificação por grupo

> Vamos criar um state para guardar a letra do grupo escolhida, criar um select, nele usar o método onChange para controlar a escolha das letras e alteração do state da letra do grupo escolhida.

1. Abra o arquivo `index.jsx`
2. Deixe o código da seguinte forma:

~~~jsx
import { useEffect, useState } from 'react'
import styles from './GroupStandings.module.css'

function GroupStandings() {

    const [ grupos, setGrupos ] = useState([])
    const [ letraSelecionada, setLetraSelecionada ] = useState('A')

    useEffect(() => {
        const buscarGrupos = async () => {
            const response = await fetch('https://raw.githubusercontent.com/edsonmaia/apifakecopa2023/main/classificacao-por-grupos-2023.json')
            const data = await response.json()
            setGrupos(data)
        }
        buscarGrupos()
    }, [])

    return (
        <>
            <div className={styles.div_select}>
                <select
                    value={letraSelecionada}
                    onChange={(e) => setLetraSelecionada(e.target.value)}>
                    <option value="A">Grupo A</option>
                    <option value="B">Grupo B</option>
                    <option value="C">Grupo C</option>
                    <option value="D">Grupo D</option>
                    <option value="E">Grupo E</option>
                    <option value="F">Grupo F</option>
                    <option value="G">Grupo G</option>
                    <option value="H">Grupo H</option>
                </select>
            </div>

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
                    grupos.filter( grupo => grupo.grupo === letraSelecionada )
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
        </>
    )
}

export default GroupStandings

~~~

## CSS de GroupStandings

1. Abra o arquivo GroupStandings.module.css
2. Abaixo do último seletor adicione a formatação da div_select e do campo select
3. Faça o seguinte código:

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

table .esquerda {
    text-align: left;
    padding-left: 1rem;
}

.div_select {
    text-align: center;
}

.div_select select {
    font-size: 1.25rem;
    padding: 10px;
    border-radius: 5px;
}

~~~

3. Salve as alterações e veja o resultado no browser.

## Refatorar o App.jsx

1. Abra o arquivo `App.jsx`
2. Vamos apagar apenas a linha da tag h2 que está dentro da div group_standings
3. Abaixo da section game_table deixe o código da seguinte forma:

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
        <GroupStandings />
      </section>

    </>

  )
}

export default App

~~~

3. Salve as alterações e veja o resultado no browser.

> Vimos nesta aula como fazer ajustes no nosso projeto para usar o filtro dinâmico que implementamos na aula anterior para fazer a exibição dos grupos após escolhermos a letra do grupo em uma caixa de seleção.

> Nas próximas aulas vamos implementar as funcionalidades sobre as fases eliminatórias - knockout stage.

Salve Devs até a próxima!
