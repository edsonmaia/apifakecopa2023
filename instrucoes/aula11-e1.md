# Projeto Copa Feminina 2023 em React JS com Vite

## Aula 11 EXTRA 1 Criar componente TabButton e Refatorar App

> Vamos abstrair a funcionalidade de botão das abas para um novo componente e em seguida iremos fazer refatorações para poder usar esse novo componente.

## Criar componente TabButton

1. Dentro da pasta `src` crie a pasta `components`
2. Dentro da pasta `components` crie a pasta `TabButton`
3. Dentro da pasta `TabButton` crie o arquivo 'index.jsx'
4. Abra o arquivo `index.jsx`
5. Deixe o código da seguinte forma:

~~~jsx
/* eslint-disable react/prop-types */
function TabButton({ tabName, activeTab, handleChangeTab}) {
    return (
        <button
            className={ activeTab === tabName ? 'active' : '' }
            onClick={() => handleChangeTab(tabName)}
        >
            {tabName}
        </button>
    )
}

export default TabButton

~~~

## Como usar o componente TabButton

1. Abra o arquivo `App.jsx`
2. Faça os seguintes ajustes:
2.1 Dentro da div .tabs apague todas as linhas de button, depois use o componente TabButton, não se esqueça do import
2.2 Na function renderTabContent mude os nomes dos cases
2.3 No useState mude o state inicial para 'Finais'
3. Deixe o código conforme o exemplo abaixo:

~~~jsx
import { useState } from 'react'
import './App.css'
import TournamentBracket from './components/TournamentBracket'
import Card from './components/Card'
import TabButton from './components/TabButton'

function App() {

  const [ activeTab, setActiveTab ] = useState('Finais')

  function handleChangeTab(tabName) {
    setActiveTab(tabName)
  }

  function renderTabContent() {
    switch(activeTab) {
      case 'Finais':
        return <TournamentBracket fase='finais' />
      case 'Semifinais':
        return <TournamentBracket fase='semifinais' />
      case 'Quartas':
        return <TournamentBracket fase='quartas' />
      case 'Oitavas':
        return <TournamentBracket fase='oitavas' />
      case 'Grupos':
        return <section className='cards'><Card /></section>
    }
  }

  return (
    <>
      <h1>Copa do Mundo Feminina 2023</h1>
      
      <section className='knockout_table'>
        
        <div className='tabs'>
          <TabButton tabName='Finais' activeTab={activeTab} handleChangeTab={handleChangeTab} />
          <TabButton tabName='Semifinais' activeTab={activeTab} handleChangeTab={handleChangeTab} />
          <TabButton tabName='Quartas' activeTab={activeTab} handleChangeTab={handleChangeTab} />
          <TabButton tabName='Oitavas' activeTab={activeTab} handleChangeTab={handleChangeTab} />
          <TabButton tabName='Grupos' activeTab={activeTab} handleChangeTab={handleChangeTab} />
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

4. Salve as alterações e faça o teste no browser.

> Veja que a aplicação continua funcionando perfeitamente, porém, agora com um novo componente.

> Nas próximas aulas, podemos implementar funcionalidades extras para nossa aplicação.

Salve Devs, até a próxima!
