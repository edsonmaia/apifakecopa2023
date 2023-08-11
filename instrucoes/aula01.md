# Projeto Copa Feminina 2023 em React JS com Vite

## Aula 01 Criar projeto + Component Card dos Grupos

1. Abra o terminal de comandos
2. Acesse a sua pasta raiz de projetos. Ex. c:\www ou c:\web
3. Digite o seguinte comando:

`npx create-vite@latest copa2023 --template react`

4. Em seguinda digite os seguintes comandos:

`cd copa2023`

`npm install`

`code .`

5. Abra o terminal de comandos `CTRL + J` ou `CTRL + '`
6. Digite o seguinte comando:

`npm run dev`

## Ajustes iniciais no projeto React com Vite

## index.html

1. Abra o arquivo index.html
2. Mude o titulo da página para
~~~html
<title>Copa do Mundo Feminina 2023</title>
~~~

3. Copie o arquivo favicon.png para a pasta public
3.1 Apague o arquivo vite.svg
3.2 Mude o código do link do favicon para:
~~~html
<link rel="icon" type="image/png" href="/favicon.png" />
~~~

4. Abaixo da tag de abertura de head cole as seguintes linhas:
~~~html
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;700&family=Roboto+Mono:wght@400;500;700&family=Victor+Mono:wght@400;500;700&display=swap" rel="stylesheet">
~~~
5. Salve as alterações

## App.jsx

1. Abra o arquivo App.jsx
2. Apague a linha 7 da const com useState
3. Apague da linha 10 até 29 o conteúdo dentro do fragment
4. Apague as três primeiras linhas:
~~~javascript
  import { useState } from 'react'
  import reactLogo from './assets/react.svg'
  import viteLogo from '/vite.svg'
~~~

5. Na linha 10 entre as tags do Frament digite o seguinte:
~~~javascript
<h1>Copa do Mundo Feminina 2023</h1>
~~~

6. Salve as alterações e veja o resultado no browser.

## App.css

1. Abra o arquivo `App.css`
2. Apague todo o conteúdo
3. Salve as alterações

## index.css (css global)

1. Abra o arquivo `index.css`
2. Apague da linha 16 até 70
3. Apague da linha 3 até a linha 9
4. Deixe o código da seguinte forma:

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

h1 {
  text-align: center;
  margin-block: 1rem;
}

~~~

5. Salve as alterações e veja o resultado no browser.

## Ajustes na página inicial App.jsx

1. Abra o arquivo App.jsx
2. Deixe a página da seguinte forma:

~~~javascript
import './App.css'

function App() {

  return (
    <>
      <h1>Copa do Mundo Feminina 2023</h1>
    </>
  )
}

export default App

~~~

3. Salve as alterações

> Vamos criar o component Card para exibir a lista de grupos

## Criar component Card

1. Dentro da pasta `src` crie a pasta `components`
2. Dentro da pasta `components` crie a pasta `Card`
3. Dentro da pasta `Card` crie os 2 arquivos 'index.jsx' e 'Card.module.css'
4. Abra o arquivo index.jsx
5. Deixe o código da seguinte forma:

~~~javascript
import styles from './Card.module.css'

function Card() {

    return (
      <section className={styles.card}>
          <div className={styles.linha}></div>
          <h2>GRUPO ?</h2>
          <ul>
            <li>
                <img src="/bandeiras/bra.png" alt="Brasil" />
                Brasil
            </li>
          </ul>
      </section>
    )
}

export default Card

~~~

6. Salve as alterações.

## Como usar o component Card

1. Abra o arquivo App.jsx
2. Abaixo da tag h1 adicione o componente Card
~~~javascript
<Card />
~~~

3. Faça o import do component Card
~~~javascript
import Card from './components/Card'
~~~

4. Salve as alterações e veja o Resultado no browser.

## CSS do component Card

1. Abra o arquivo Card.module.css
2. Faça o seguinte código:

~~~css
.card {
    width: 200px;
    height: 265px;
    background-color: #f1f1f1;
    box-shadow: 5px 5px 10px #ccc;
}

.card .linha {
    width: 100%;
    height: 10px;
}

.card h2 {
    text-align: center;
    margin-top: 0.75rem;
    margin-bottom: 0.5rem;
}

.card ul {
    margin-left: 1rem;
}

.card ul li {
    list-style: none;
    display: flex;
    gap: 0.5rem;
    align-items: center;
    line-height: 50px;
}

~~~

3. Salve as alterações e veja o resultado no browser.

## Cards Dinâmicos dos Grupos da Copa

1. Abra o arquivo index.jsx do component Card
2. Refatore o código para ficar da seguinte forma:

~~~javascript
import { useEffect, useState } from 'react'
import styles from './Card.module.css'

function Card() {

    const [ grupos, setGrupos ] = useState([])

    useEffect(() => {
        const buscarGrupos = async () => {
            const response = await fetch('https://raw.githubusercontent.com/edsonmaia/apifakecopa2023/main/selecoes.json')
            const data = await response.json()
            setGrupos(data)
        }
        buscarGrupos()
    }, [])

    return (
        grupos.map( grupo => 
            <section className={styles.card} key={grupo.grupo}>
                <div className={styles.linha} style={{'backgroundColor': grupo.cor}}></div>
                <h2>GRUPO {grupo.grupo}</h2>
                <ul>
                    {
                        grupo.selecoes.map( pais => {
                          return (
                            <li key={pais.sigla}>
                                <img src={`/bandeiras/${pais.imagem}.png`} alt={pais.selecao} />
                                {pais.selecao}
                            </li>
                            ) 
                        })
                    }
                </ul>
            </section>
        )
    )
}

export default Card

~~~

3. Salve as alterações e veja o resultado no browser.

## CSS da class .cards de App.css

1. Abra o arquivo App.css
2. Faça o seguinte código css:

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

~~~

3. Salve as alterações e veja o resultado no browser.

> Vimos nesta aula como criar um projeto React com Vite, além de fazer ajustes da página App (página principal da aplicação) e também como criar o componente Card para exibir as informações de cada um dos oito grupos da copa, vimos também como usar useState e useEffect, fazer requisição assíncrona para obter os dados para criar os cards dinamicamente.
> Na próxima aula vamos ver como criar a tabela de jogos.

Salve Devs até a próxima!
