# Projeto Copa Feminina 2023 em React JS com Vite

## Aula 06 Usar Componente KnockoutStage

> Vamos usar o component KnockoutStage (Fase Eliminatória) para exibir cards com os jogos das fases eliminatórias seguintes, hoje veremos das quartas de final.

> Mas, antes vamos refatorar uma linha do código que ficou pendente na aula anterior. Na linha 24 onde está a tag h2 da section jogo que está com a palavra Oitavas, vamos substituir a palavra Oitavas pela props {fase}.

## Refatorar o arquivo index.jsx de KnockoutStage

1. Abra o arquivo `index.jsx` de `KnockoutStage`
2. Substitua a palavra `Oitavas` por `{fase}`

~~~jsx
  <h2 className={styles.titulo2}>{fase} {jogo.jogo} - chave {jogo.chave}</h2>
~~~

3. Salve as alterações e feche o arquivo

## Como usar o componente KnockoutStage para as Quartas

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

      <h2>Quartas de Final</h2>

      <section className='knockout_table'>
        <KnockoutStage fase="quartas" />
      </section>

    </>

  )
}

export default App

~~~

3. Salve as alterações e veja o resultado no browser.

## Desafio de código


> Vimos nesta aula como refatorar e usar o componente KnockoutStage no nosso projeto para criar cards que mostrem as partidas das fases eliminatórias das quartas de final. Mas, vou deixar um desafio de código para vocês.

Desenvolva um componente que use os conceitos do KnockoutStage que usa props, para exibir a "lista de jogos do dia". O nome do componente pode ser Fixture ou FixtureList. Uma dica, é importante usar a data do evento como uma props.

> Nas próximas aulas vamos implementar mais recursos do nosso projeto.

Salve Devs até a próxima!
