# Projeto Copa Feminina 2023 em React JS com Vite

## Aula 07 Criar Componente Fixture

> Vamos criar o component Fixture (Lista de Jogos do Dia) para exibir cards com os jogos do dia com base em uma data que é repassada pelo usuário.

> Mas, antes vamos refatorar uma linha do código das aulas anteriores. Na linha 24 onde está a tag h2 da section jogo.

## Refatorar o arquivo index.jsx de KnockoutStage

1. Abra o arquivo `index.jsx` de `KnockoutStage`
2. Substitua o trecho `{fase}` por `{ jogo.tipo == "decisão" ? jogo.fase : fase }`

~~~javascript
  <h2 className={styles.titulo2}>{ jogo.tipo == "decisão" ? jogo.fase : fase } {jogo.jogo} - chave {jogo.chave}</h2>
~~~

> Isto serve para otimizar a exibição dos cards da disputa do terceiro lugar e da final. Também pode ser simplificado pela seguinte linha sem a verifição do tipo:

~~~javascript
  <h2 className={styles.titulo2}>{ jogo.fase } {jogo.jogo} - chave {jogo.chave}</h2>
~~~

3. Salve as alterações e feche o arquivo

## Como criar o componente Fixture

1. Dentro da pasta `src` crie a pasta `components`
2. Dentro da pasta `components` crie a pasta `Fixture`
3. Dentro da pasta `Fixture` crie os 2 arquivos 'index.jsx' e 'Fixture.module.css'
4. Abra o arquivo `index.jsx`

> Copie todo o código jsx do componente KnockoutStage. Só iremos mudar algumas linhas e nomes:

4.1 Linha 2 mude só o nome do link do css
4.2 Linha 5 mude o nome da function e adicione a props data
4.3 Linha 19 adicione uma variável para guardar os jogosFiltrados por meio do filter de data
4.4 Linhas 24 e 25 faça uma condicional para ver se tem jogos fazer o mapeamento
4.5 Linha 71 faça o senão da condicional para exibir uma mensagem que não tem jogos no dia

5. Deixe o código da seguinte forma:

~~~javascript
/* eslint-disable react/prop-types */
import { useEffect, useState } from 'react'
import styles from './Fixture.module.css'

function Fixture({ fase, data }) {

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

    let jogosFiltrados = jogos.filter( jogo => jogo.data == data )

    return (
        <section className={styles.jogos}>
            {
                (jogosFiltrados.length > 0) ?
                jogosFiltrados.map( jogo => (
                    <div
                        key={jogo.jogo}
                        className={styles.jogo} >
                        <h2 className={styles.titulo2}>
                            { jogo.tipo == "decisão" ? jogo.fase : fase } {jogo.jogo} - chave {jogo.chave}
                        </h2>
                        <h3>
                            <span className={styles.dia}>{jogo.dia}</span>
                            <span className={styles.data}>{jogo.data}</span>
                            <span className={styles.hora}>{jogo.hora}</span>
                        </h3>
                        <h3 className={styles.placar}>
                            <div className={styles.mandante_box}>
                                {jogo.mandante}
                                <img src={`/bandeiras/${jogo.sigla_mandante.toLowerCase()}.png`} alt={jogo.mandante} />
                            </div>
                            <div className={styles.placar_box}>
                                <span className={styles.gols}>{jogo.gols_mandante}</span>
                                x
                                <span className={styles.gols}>{jogo.gols_visitante}</span>
                            </div>
                            <div className={styles.visitante_box}>
                                <img src={`/bandeiras/${jogo.sigla_visitante.toLowerCase()}.png`} alt={jogo.visitante} />
                                {jogo.visitante}
                            </div>
                        </h3>
                        <div className={`${styles.tempo_extra} ${styles.centralizar}`}>
                            {
                                jogo.prorrogacao === "Sim" &&
                                <div>
                                    Prorrogação? {jogo.prorrogacao} | 
                                    Placar {jogo.placar_prorrogacao}
                                </div>
                            }
                            {
                                jogo.penaltis === "Sim" &&
                                <div>
                                    Pênaltis? {jogo.penaltis} | 
                                    Placar {jogo.placar_penaltis}
                                </div>
                            }
                        </div>
                        <h4>Vencedor: {jogo.vencedor}</h4>
                    </div>
                ))
                : <h4>Sem jogos no dia {data}</h4>
            } 
        </section>
    )
}

export default Fixture

~~~

3. Salve as alterações e veja o resultado no browser.

## CSS de Fixture

> Todo o código CSS de Fixture será o mesmo do componente KnockoutStage, só copie e cole ele no arquivo.

## Como usar o componente Fixture

## Como usar o componente KnockoutStage

1. Abra o arquivo App.jsx
2. No final do return adicione uma tag h1 comente as linha de código 13 até 33, comente também das linhas 3 até 5 dos importes e deixe o código da seguinte forma:

~~~javascript
import './App.css'
import Fixture from './components/Fixture'
// import Card from './components/Card'
// import GameTable from './components/GameTable'
// import GroupStandings from './components/GroupStandings'
import KnockoutStage from './components/KnockoutStage'

function App() {

  return (
    <>
      <h1>Copa do Mundo Feminina 2023</h1>

      {/* <section className='cards'>
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
      </section> */}

      <h2>Jogos do dia 10/08/2023</h2>

      <section className='knockout_table'>
        <Fixture fase="quartas" data="10/08" />
      </section>

      <h2>Quartas de Final</h2>

      <section className='knockout_table'>
        <KnockoutStage fase="quartas" />
      </section>

      <h2>Semifinais</h2>

      <section className='knockout_table'>
        <KnockoutStage fase="semifinais" />
      </section>

      <h2>Finais</h2>

      <section className='knockout_table'>
        <KnockoutStage fase="finais" />
      </section>
      
    </>

  )
}

export default App

~~~

> Perceba que você agora utiliza o componente Fixture passando duas props, a primeira é o nome da rodada que vai servir para pegar os dados do json (da nossa api fake) e a segunda props é a data, sendo dia/mês que é a data do jogo.

## Dicas finais

> Vimos nesta aula uma proposta de solução para o desafio da aula anterior de desenvolver um componente que use os conceitos do KnockoutStage que usa props, para exibir a "lista de jogos do dia". O nome do componente pode ser Fixture ou FixtureList. Uma dica, é importante usar a data do evento como uma props.
> Vimos também uma refatoração do componente KnockoutStage para mostrar o nome da fase que vêm lá do arquivo json e não o nome da fase que vem da props, para que o componente possa ser usado nas fases de decisão do terceiro e na grande final.

> Nas próximas aulas vamos implementar mais recursos do nosso projeto.

Salve Devs até a próxima!
