# Projeto Copa Feminina 2023 em React JS com Vite

## Aula 10 Refatoração e Deploy na Vercel

> Na última aula fizemos o recurso de navegação por abas, nesta aula vamos aumentar a quantidade de abas e fazer uma pequena refatoração para solucionar um problema de renderização dos jogos.

### Ampliar a quantidade de abas

> Vamos criar novos cases no switch e novos buttons para exibir mais abas de finais e grupos.

Dentro do diretório do seu projeto, navegue até o arquivo src/App.js e substitua o conteúdo pelo seguinte código:

~~~jsx
import { useState } from 'react'
import './App.css'
import TournamentBracket from './components/TournamentBracket'
import Card from './components/Card'

function App() {

  const [ activeTab, setActiveTab ] = useState('Tab 1')

  function handleChangeTab(tabName) {
    setActiveTab(tabName)
  }

  function renderTabContent() {
    switch(activeTab) {
      case 'Tab 1':
        return <TournamentBracket fase='finais' />
      case 'Tab 2':
        return <TournamentBracket fase='semifinais' />
      case 'Tab 3':
        return <TournamentBracket fase='quartas' />
      case 'Tab 4':
        return <TournamentBracket fase='oitavas' />
      case 'Tab 5':
        return <section className='cards'><Card /></section>
    }
  }

  return (
    <>
      <h1>Copa do Mundo Feminina 2023</h1>
      
      <section className='knockout_table'>
        
        <div className='tabs'>
          <button
            className={ activeTab === 'Tab 1' ? 'active' : '' }
            onClick={() => handleChangeTab('Tab 1')}
          >
            Finais
          </button>
          <button
            className={ activeTab === 'Tab 2' ? 'active' : '' }
            onClick={() => handleChangeTab('Tab 2')}
          >
            Semifinais
          </button>
          <button
            className={ activeTab === 'Tab 3' ? 'active' : '' }
            onClick={() => handleChangeTab('Tab 3')}
          >
            Quartas
          </button>
          <button
            className={ activeTab === 'Tab 4' ? 'active' : '' }
            onClick={() => handleChangeTab('Tab 4')}
          >
            Oitavas
          </button>
          <button
            className={ activeTab === 'Tab 5' ? 'active' : '' }
            onClick={() => handleChangeTab('Tab 5')}
          >
            Grupos
          </button>
        </div>

        <div className='tab_content'>
          { renderTabContent() }
        </div>

      </section>

    </>
  )
}

export default App

~~~

Salve as alterações e faça o teste no browser. Perceba que teremos um 'problema', a informação sobre a disputa do terceiro lugar continua aparecendo mesmo quando clicamos em outras abas das fases eliminatórias. Isso é um problema na key do nosso componente TournamentBracket.

## Solução do problema na key

1. Abra o arquivo `index.jsx` do componente `TournamentBracket`
2. Mude apenas a linha 28 do código que tem a div com a key, ao invés de jogo.jogo, use jogo.id

~~~jsx
  <div key={jogo.id} className={styles.jogo}>
~~~

3. Veja abaixo como deve ficar o código completo do arquivo:

~~~jsx
/* eslint-disable react/prop-types */
import { useState, useEffect } from 'react'
import styles from './TournamentBracket.module.css'
import HeaderComponent from '../HeaderComponent'
import DateTimeComponent from '../DateTimeComponent'
import ScoreComponent from '../ScoreComponent'
import ExtraInfoComponent from '../ExtraInfoComponent'
import WinnerComponent from '../WinnerComponent'

function TournamentBracket({ fase }) {

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
                    <div key={jogo.id} className={styles.jogo}>
                        <HeaderComponent jogo={jogo} />
                        <DateTimeComponent jogo={jogo} />
                        <ScoreComponent jogo={jogo} />
                        <ExtraInfoComponent jogo={jogo} />
                        <WinnerComponent jogo={jogo} />
                    </div>
                ))
            }
        </section>
    )
}

export default TournamentBracket

~~~

4. Salve as alterações e faça o teste no browser.

> É recomendável que você atualize a props key também dos compomentes KnockoutStage e Fixture, pois, fizemos eles utilizando a key={jogo.jogo} mude para key={jogo.id} Assim não teremos mais problemas do tipo no nosso projeto.

## Deploy na Vercel

1. Publique sua aplicação React JS da Copa em um repositório do `GitHub`
2. Acesse o site da vercel https://vercel.com/
3. Clique no botão `Start Deploying`
4. Na tela `Import Git Repository` clique no botão `Continue with GitHub`
5. Faça o login na Vercel utilizando a sua conta do GitHub
6. Procure o seu repositório copa2023 na lista, depois clique no botão `Import`
7. Digite o nome do projeto. Ex.: `copa2023`
8. Clique no botão `Deploy`

> Após poucos segundos ou minutos o deploy estará concluído com sucesso!

9. Clique na imagem abaixo do Congratulations para abrir em uma nova aba o seu projeto que está publicado.

> Se quiser ver mais detalhes do seu projeto clique no botão `Continue to Dashboard`

> Nas próximas aulas, podemos implementar funcionalidades extras para nossa aplicação.

Salve Devs, até a próxima!
