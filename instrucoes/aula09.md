# Projeto Copa Feminina 2023 em React JS com Vite

## Navegação por Abas

> Trabalhar com navegação por abas em um projeto ReactJS é uma tarefa comum e pode ser feita de várias maneiras, dependendo das suas necessidades. Vamos ver um exemplo básico de como implementar a navegação por abas usando componentes e estados do React.
> Suponha que você queira criar uma página com três abas: "Tab 1", "Tab 2" e "Tab 3", e exibir conteúdo diferente em cada uma delas.

### Implementando a Navegação por Abas

Dentro do diretório do seu projeto, navegue até o arquivo src/App.js e substitua o conteúdo pelo seguinte código:

~~~jsx
import { useState } from 'react'
import './App.css'

function App() {

  const [activeTab, setActiveTab] = useState('Tab 1')

  function handleChangeTab(tabName) {
    setActiveTab(tabName)
  }

  function renderTabContent() {
    switch (activeTab) {
      case 'Tab 1':
        return <TournamentBracket fase='semifinais' />
      case 'Tab 2':
        return <TournamentBracket fase='quartas' />
      case 'Tab 3':
        return <TournamentBracket fase='oitavas' />
      default:
        return null
    }
  }

  return (
    <div className="App">
      <div className="tabs">
        <button
          className={activeTab === 'Tab 1' ? 'active' : ''}
          onClick={() => handleChangeTab('Tab 1')}
        >
          Tab 1
        </button>
        <button
          className={activeTab === 'Tab 2' ? 'active' : ''}
          onClick={() => handleChangeTab('Tab 2')}
        >
          Tab 2
        </button>
        <button
          className={activeTab === 'Tab 3' ? 'active' : ''}
          onClick={() => handleChangeTab('Tab 3')}
        >
          Tab 3
        </button>
      </div>

      <div className="tab_content">
        {renderTabContent()}
      </div>

    </div>
  );
}

export default App

~~~

> O nome da função handleChangeTab deveria ser handleTabChange, este nome ficaria com a grafia mais adequada.

## CSS no arquivo App.css

Adicione o seguinte código a partir da linha 17:

~~~css
/* abas */
body {
    background-color: #ececec;
}

.tabs {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 1rem;
    margin-bottom: 1rem;
}

.tabs button {
    border: 1px solid #ccc;
    border-radius: 8px;
    padding: 10px;
    font-weight: bold;
    cursor: pointer;
}

.tabs button.active {
    background-color: #111;
    color: #fff;
}

~~~

Salve as alterações e veja o resultado no browser.

> Nesta aula vimos de forma rápida como implementar a funcionalidade de navegação por abas, ela usa vários conceitos do React JS, sem o uso de libs de terceiros, nem controle de rotas.
> Outro ponto relevante é que os botões que criamos podem ser novos compomentes. Toda vez que você perceber códigos repetidos, ali tem um grande potencial de você refatorar e tornar um novo componente.
Nas próximas aulas vamos implementar mais funcionalidades para nossa aplicação.

Salve Devs, até a próxima!
