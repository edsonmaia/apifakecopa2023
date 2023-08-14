# Projeto Copa Feminina 2023 em React JS com Vite

## Aula 08 Composição de componentes

> A composição de componentes é uma abordagem fundamental em React para construir interfaces reutilizáveis e modularizar seu código. Ela permite que você divida a interface do usuário em componentes menores e independentes, que podem ser combinados para criar componentes mais complexos. Vou te mostrar como você pode aplicar a composição de componentes ao seu código existente.

> Vamos criar um novo componente chamado TournamentBracket e dividi-lo em componentes menores e reutilizáveis

## Criar componente 'pai' ou 'mãe'

1. Dentro da pasta `src` crie a pasta `components`
2. Dentro da pasta `components` crie a pasta `TournamentBracket`
3. Dentro da pasta `TournamentBracket` crie os 2 arquivos 'index.jsx' e 'TournamentBracket.module.css'
4. Abra o arquivo `index.jsx`
5. Use o mesmo código do componente `KnockoutStage` e deixe o código da seguinte forma:

~~~jsx
/* eslint-disable react/prop-types */
import { useEffect, useState } from 'react'
import styles from './TournamentBracket.module.css'

function TournamentBracket( { fase } ) {
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
                <div key={jogo.jogo} className={styles.jogo}>
                    <h2 className={styles.titulo2}>
                        { jogo.fase } {jogo.jogo} - chave {jogo.chave}
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
                    <div className={styles.centralizar}>
                        {jogo.prorrogacao === 'Sim' && (
                          <div className={styles.centralizar}>
                            <span>Prorrogação? {jogo.prorrogacao} | Placar Prorrogação: {jogo.placar_prorrogacao}</span>
                          </div>
                        )}
                        {jogo.penaltis === 'Sim' && (
                          <div className={styles.centralizar}>
                            <span>Pênaltis? {jogo.penaltis} | Placar Pênaltis: {jogo.placar_penaltis}</span>
                          </div>
                        )}
                    </div>                        
                    <h4>Vencedor: {jogo.vencedor}</h4>
                </div>
            ))
        }
    </section>
)
}

export default TournamentBracket

~~~

> Agora vamos separar esse componente maior em componentes menores - HeaderComponent, DateTimeComponent, ScoreComponent, ExtraInfoComponent

> Crie uma pasta para cada componente, com seu arquivo index.jsx

### HeaderComponent: Um componente para exibir o cabeçalho de cada jogo.

~~~jsx
/* eslint-disable react/prop-types */
import styles from './HeaderComponent.module.css'

function HeaderComponent({ jogo }) {
    return (
        <h2 className={styles.titulo2}>
            { jogo.fase } {jogo.jogo} - chave {jogo.chave}
        </h2>
    )
}

export default HeaderComponent

~~~

### DateTimeComponent: Um componente para exibir a data e hora de cada jogo.

~~~jsx
/* eslint-disable react/prop-types */
import styles from './DateTimeComponent.module.css'

function DateTimeComponent({ jogo }) {
  return (
    <h3>
      <span className={styles.dia}>{jogo.dia}</span>
      <span className={styles.data}>{jogo.data}</span>
      <span className={styles.hora}>{jogo.hora}</span>
    </h3>
  )
}

export default DateTimeComponent

~~~

### ScoreComponent: Um componente para exibir o placar e as equipes de cada jogo.

~~~jsx
/* eslint-disable react/prop-types */
import styles from './ScoreComponent.module.css'

function ScoreComponent({ jogo }) {
  return (
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
  )
}

export default ScoreComponent

~~~

### ExtraInfoComponent: Um componente para exibir informações extras sobre o jogo, como prorrogação e pênaltis.

~~~jsx
/* eslint-disable react/prop-types */
import styles from './ExtraInfoComponent.module.css'

function ExtraInfoComponent({ jogo }) {
  return (
    <div className={styles.centralizar}>
      {jogo.prorrogacao === 'Sim' && (
        <div className={styles.centralizar}>
          <span>Prorrogação? {jogo.prorrogacao} | Placar Prorrogação: {jogo.placar_prorrogacao}</span>
        </div>
      )}
      {jogo.penaltis === 'Sim' && (
        <div className={styles.centralizar}>
          <span>Pênaltis? {jogo.penaltis} | Placar Pênaltis: {jogo.placar_penaltis}</span>
        </div>
      )}
    </div>
  )
}

export default ExtraInfoComponent

~~~

### WinnerComponent.jsx: Um componente para exibir o vencedor de cada jogo.

~~~jsx
/* eslint-disable react/prop-types */
import styles from './WinnerComponent.module.css'

function WinnerComponent({ jogo }) {
  return <h4>Vencedor: {jogo.vencedor}</h4>
}

export default WinnerComponent

~~~

## Como organizar os componentes 'menores'

Após dividir o componente `TournamentBracket` em componentes menores, você pode reorganizá-los para criar o componente utilizando a composição de componentes:

~~~jsx
import { useEffect, useState } from 'react'
import styles from './TournamentBracket.module.css'
import HeaderComponent from '../HeaderComponent'
import DateTimeComponent from '../DateTimeComponent'
import ScoreComponent from '../ScoreComponent'
import ExtraInfoComponent from '../ExtraInfoComponent'
import WinnerComponent from '../WinnerComponent'

function TournamentBracket({ fase }) {
  const [jogos, setJogos] = useState([])
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
      {jogos.map((jogo) => (
        <div key={jogo.jogo} className={styles.jogo}>
          <HeaderComponent fase={jogo.fase} jogo={jogo.jogo} />
          <DateTimeComponent jogo={jogo} />
          <ScoreComponent jogo={jogo} />
          <ExtraInfoComponent jogo={jogo} />
          <WinnerComponent jogo={jogo} />
        </div>
      ))}
    </section>
  )
}

export default TournamentBracket

~~~

## Como usar o componente TournamentBracket

1. Abra o arquivo `App.jsx`
2. Faça os seguintes ajustes no código:

~~~jsx
import './App.css'
import TournamentBracket from './components/TournamentBracket'

function App() {

  return (
    <>
      <h1>Copa do Mundo Feminina 2023</h1>

      <section className='knockout_table'>
        <h2>Finais</h2>
        <TournamentBracket fase='finais' />

        <h2>Semifinais</h2>
        <TournamentBracket fase='semifinais' />

        <h2>Quartas</h2>
        <TournamentBracket fase='quartas' />

        <h2>Oitavas</h2>
        <TournamentBracket fase='oitavas' />
      </section>
      
    </>

  )
}

export default App

~~~

3. Salve as alterações e veja o resultado no browser.

> Agora, o seu componente TournamentBracket é construído a partir da combinação de componentes menores e mais especializados, seguindo o princípio da composição de componentes do React. Isso torna o código mais legível, reutilizável e fácil de manter.

Salve Devs, até a próxima!
