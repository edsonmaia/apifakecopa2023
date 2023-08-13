# Projeto Copa Feminina 2023 em React JS com Vite

## Aula 05 Componente KnockoutStage

> Vamos criar o component KnockoutStage (Fase Eliminatória) para exibir cards com os jogos das fases eliminatórias - oitavas, quartas, semi, terceiro e final.

## Criar component KnockoutStage

1. Dentro da pasta `src` crie a pasta `components`
2. Dentro da pasta `components` crie a pasta `KnockoutStage`
3. Dentro da pasta `KnockoutStage` crie os 2 arquivos 'index.jsx' e 'KnockoutStage.module.css'
4. Abra o arquivo `index.jsx`
5. Deixe o código da seguinte forma:

~~~jsx
/* eslint-disable react/prop-types */
import { useState, useEffect } from 'react'
import styles from './KnockoutStage.module.css'

function KnockoutStage( { fase } ) {

    const [ jogos, setJogos ] = useState([])
    const url = `https://raw.githubusercontent.com/edsonmaia/apifakecopa2023/main/${fase}-copa-2023.json`

    useEffect(() => {
        const buscarJogos = async () => {
            const response = await fetch(url)
            const data = await response.json()
            setJogos(data)
        }
        buscarJogos()
    }, [url])

    return (
        <section className={styles.jogos}>
            {
                jogos.map( jogo => (
                    <section className={styles.jogo} key={jogo.jogo}>
                        <h2 className={styles.titulo2}>Oitavas {jogo.jogo} - chave {jogo.chave}</h2>
                        <h3 className={styles.jogo_detalhes}>
                            <span className={styles.dia}>{jogo.dia}</span>
                            <span className={styles.data}>{jogo.data}</span>
                            <span className={styles.hora}>{jogo.hora}</span>
                        </h3>
                        <h3 className={styles.placar}>
                            <div className={styles.mandante_box}>
                                {jogo.mandante}
                                <img src={`/bandeiras/${jogo.sigla_mandante.toLowerCase()}.png`} alt="{jogo.mandante}" />
                            </div>
                            <div className={styles.placar_box}>
                                <span className={styles.gols}>{jogo.gols_mandante}</span>
                                x
                                <span className={styles.gols}>{jogo.gols_visitante}</span>
                            </div>
                            <div className={styles.visitante_box}>
                                <img src={`/bandeiras/${jogo.sigla_visitante.toLowerCase()}.png`} alt="{jogo.visitante}" />
                                {jogo.visitante}
                            </div>
                        </h3>
                        <div className={styles.tempo_extra}>
                            {
                            jogo.prorrogacao == "Sim" &&
                            <div className={styles.centralizar}>
                                <span>Prorrogação? {jogo.prorrogacao} | Placar Prorrogação: {jogo.placar_prorrogacao}</span>
                                <span>Pênaltis? {jogo.penaltis} | Placar Pênaltis: {jogo.placar_penaltis}</span>
                            </div>
                            }
                        </div>
                        <h4>Vencedor: {jogo.vencedor}</h4>
                    </section>
                ))
            }
        </section>
    )
}

export default KnockoutStage

~~~

## CSS de KnockoutStage

1. Abra o arquivo `KnockoutStage.module.css`
2. Faça o seguinte código:

~~~css
.jogo {
    border: 1px solid #eee;
    background-color: #f2f2f2;
    box-shadow: 5px 5px 10px #ccc;
    margin-bottom: 1rem;
}

.titulo2 {
    font-size: 1rem;
    font-weight: 400;
}

.jogo_detalhes {
    display: flex;
    align-items: center;
    justify-content: center;
    margin-left: 15px;
}

.dia, .data, .hora {
    font-size: 1rem;
    border-radius: 8px;
    padding: 5px 8px;
}

.data {
    background-color: #111;
    color: #fff;
}

.placar {
    display: flex;
    justify-content: center;
    align-items: center;

    width: 100%;
}

.mandante_box, .visitante_box, .placar_box {
    display: flex;
    align-items: center;
    gap: 1rem;
}

.placar_box {
    min-width: 55px;
    justify-content: center;
    font-size: 12px;
    color: #555;
    gap: 0.5rem;
}

.mandante_box {
    width: 100%;
    margin-right: 1rem;
    justify-content: flex-end;
}

.visitante_box {
    width: 100%;
    margin-left: 1rem;
    justify-content: flex-start;
}

.gols {
    font-size: 1.5rem;
    color: #222;
}

.centralizar {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
}

~~~

3. Salve as alterações e veja o resultado no browser.

## Como usar o componente KnockoutStage

1. Abra o arquivo App.jsx
2. No final do return adicione uma tag h2 e o componente, deixe o código da seguinte forma:

~~~jsx
import './App.css'
import Card from './components/Card'
import GameTable from './components/GameTable'
import GroupStandings from './components/GroupStandings'
import KnockoutStage from './components/KnockoutStage'

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

      <h2>Classificação por Grupo</h2>

      <section className='group_table'>
        <GroupStandings />
      </section>

      <h2>Oitavas de Final</h2>

      <section className='knockout_table'>
        <KnockoutStage fase="oitavas" />
      </section>

    </>

  )
}

export default App

~~~

3. Salve as alterações e veja o resultado no browser.

## Ajustes no App.css

1. Abra o arquivo `App.css`
2. Deixe o código da seguinte forma:

~~~css
.cards {
    max-width: 1000px;
    display: flex;
    flex-wrap: wrap;
    gap: 1rem;
    align-items: center;
    justify-content: center;

    margin: auto;
}

.knockout_table {
    max-width: 1000px;
    margin: auto;
}

~~~

## Ajustes no index.css

1. Abra o arquivo `index.css`
2. Deixe o código da seguinte forma:

~~~css
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

:root {
  font-family: Inter, sans-serif;

  font-synthesis: none;
  text-rendering: optimizeLegibility;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  -webkit-text-size-adjust: 100%;
}

h1, h2, h3, h4, h5, h6 {
  text-align: center;
  margin-block: 1rem;
}

h4, h5, h6 {
  font-size: 1rem;
}

~~~

3. Salve as alterações e veja o resultado browser.

> Vimos nesta aula como criar o componente KnockoutStage no nosso projeto para criar cards que mostrem as partidas das fases eliminatórias, oitavas, quartas, semi, terceiro lugar e final.

> Nas próximas aulas vamos implementar mais recursos do nosso projeto.

Salve Devs até a próxima!
