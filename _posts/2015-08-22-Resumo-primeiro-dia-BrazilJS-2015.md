---
layout: post
title: "Resumo do primeiro dia do BrazilJS 2015"
date: 2015-08-22
comments: true
categories: programming javascript
---

Daí pessoal, tudo certo? Resolvi fazer este post com um pequeno resumo das palestras do primeiro dia do BrazilJS 2015.
É importante destacar que tudo aqui escrito vem da minha experiência do evento e de tudo aquilo que pude absorver e/ou achei interessante o bastante para comentar.

Espero que atenda as tuas expectativas!

## Palestra 1 - Christian Heilmann - ES6 - Baseline para a web moderna?

O Chris procurou falar sobre dois pilares bastante discutidos entre desenvolvedores JavaScript: a nova versão do ECMAScript, o ES6 e sobre comos precisamos depositar todos os nossos esforços em trazer a maior quantidade de boas funcionalidades para o browser ao invés de ficar "apenas" criando frameworks, bibliotecas e trabalhando com JavaScript em ambientes fechados como no NodeJS.
Alguns pontos interessantes que ele levantou:

* Utilize novos frameworks com uma visão crítica e não se torne simplesmente um fanboy de uma determinada tecnologia
* "This is not a fight against innovation", se referindo aos grandes browsers do mercado (Firefox, Chrome, Edge e Safari)
* "Deliver code to user above everything" e a "Priority of Constituencies" (preferência máxima pelo usuário definido no draft dos princípios de design do HTML da W3C). Aqui ele basicamente diz que por mais que o ES6 deva ser utilizado "in the wild" os browsers antigos precisam continuar suportando e para isso a única saída é a transpilação, o que ele também considera ruim. É UM GRANDE DILEMA!
* Ser contra empresas que exploram o open source para fazer as suas próprias soluções fechadas para aplicativos que já conhecemos. O principal exemplo disso são as grandes fabricantes de smartphones que criam as suas próprias versões de browsers.
* "There are people missing the great things in the web". Aqui ele comenta um pouco sobre os desenvolvedores que não exploram tudo de novo que está surgindo e continuam outdated.
* O comentário mais importante dele: "quando as coisas deixaram de ser desenvolvidas para produção?", se referindo a bibliotecas e frameworks em JS que não eram consideradas production-ready
* No final das contas ele basicamente "detona" a ideia de transpilar código ES6 para ES5, frameworks como Angular e React e ambientes fechados como o que temos em NodeJS. O que ele defende é utilizar o ES6 diretamente e principalmente no browser. Por mais que se diga que essas funcionalidades são muito novas e estariam lentas ou com problemas a ideia do Chris seria utilizá-las o quanto antes com dados reais numa aplicação real para que os problemas possam ser encontrados e corrigidos e os bottlenecks de performance possam ser elimininados.
Alguns links:
	* [A boa e velha tabela de compatibilidade do ES6](https://kangax.github.io/compat-table/es6/) 
	* [Testes para "conformance" das funcionalidades do ES](https://github.com/tc39/test262)
	* [Testes de performance para do ES6](http://kpdecker.github.io/six-speed/) (várias funcionalidades estão lentas mas vão melhorar com o tempo, naturalmente)

## Palestra 2 - Douglas Campos - Use lowlevel

Bottom-line do talk: conheca e trabalhe com o baixo nível, isso vai te tornar um desenvolvedor melhor.
Alguns pontos legais levantados durante a palestra:

* "Those who don't know history are doomed to repeat it.", se referindo a pessoas que não se deparam com problemas de baixo nível e acabam cometendo os mesmos erros que já foram cometidos há 20 anos atrás (ou mais)
* Saiba mais sobre compiladores, browsers, frameworks.
* "Don't be afraid of lowlevel"

## Palestra 3 - Felipe Ribeiro - JavaScript @ Spotify

Palestra bastante esperada, o Felipe nos conta em detalhes toda a história do aplicativo do Spotify para o desktop e como ocorreu a última migração para um codebase 100% web com JS.

Alguns pontos:

* A primeira versão da aplicação ficou sem utilização por 1 ano até que as gravadoras começassem a gradativamente aceitar o Spotify
* O Chromium Embedded Framework (CEF) utilizado na aplicação é o mesmo que deu a base para o node-webkit e também é utilizado em aplicações como o Steam e o Slack.
* O Spotify ainda usa iframes!! Sim, mas há um motivo: a remoção dos iframes causaria um risco e um esforço muito maior no projeto de migração da tecnologia, então eles optaram por deixar assim por enquanto e removê-los com mais calma futuramente
* O codebase da aplicação está num único repositório e não separado em vários. No começo tentou-se criar um repositório para cada feature (playlist, radio, search) mas a fragmentação causou um esforço muito maior do desenvolvimento e eles optaram por unificar tudo.
Basicamente esta foi uma situação dentre muitas outras onde o monolito imperou sobre o novo conceito de microserviços. É a vida!

## Palestra 4 - Damian Schenkelman - Getting over Moore's Law: Parallelization using JavaScript in the browser

O Damian fala aqui basicamente sobre Web Workers, Paralelização e Concorrência em JavaScript. Sou um completo ignorante nestes tópicos e portanto não tecerei muitos comentários.
Quem sabe, sabe. Quem não sabe (como eu) que estude!

* Web Workers
* função postMessage()
* Typed Arrays
* Links:
	* [Transferrable vs cloning](https://jsperf.com/transferrable-vs-cloning/2)
	* [SIDM sum](https://jsperf.com/simd-sum)
	* [Link para a talk](https://github.com/dschenkelman/parallelism-js-talk)

## Palestra 5 - Reinaldo Ferraz - A saga dos 12 tópicos de acessibilidade

Palestra bem técnica com relação a elementos de acessibilidade de um cara especialista no assunto.

[Apresentação aqui](http://pt.slideshare.net/reinaldoferraz/a-saga-dos-12-tpicos-de-acessibilidade-na-web).

## Palestra 6 - Tania Gonzalez - The Javascript Toolkit

A Tania da TW falou sobre o JavaScript Toolkit, um compilado de diversos frameworks, bibliotecas e ferramentas para se trabalhar com o JavaScript. Para visualizar este compilado [clique aqui](https://github.com/bymarkone/javascript-toolkit).

## Palestra 7 - Raphael Amorim - 500 days of open source

Aqui o Raphael basicamente faz uma palestra motivacional com o intuito de tirar nós, os desenvolvedores, de suas zonas-de-conforto e aprender mais e mais da forma que acharmos melhor. A ideia central é ter foco e manter um padrão ritmado de estudos para alcançar os nossos objetivos, seja ele o que for: aprender uma nova linguagem, técnica, pattern, framework, biblioteca, o que for!

No final ele comentou de um projeto criado por ele e mais alguns amigos que busca ajudar nesse objetivo, o Write Code Everyday. Para saber mais, [clique aqui](http://writecodeeveryday.io/).

## Palestra 8 - Nicolas Bevacqua - High Performance in the Critical Rendering Path

Seria praticamente uma ofensa tentar resumir essa talk nesse post. A quantidade de conteúdo foi enorme, mas o resumo é o seguinte: o Nicolas explicou várias técnicas e divulgou vários plugins que buscam tornar a performance de um site melhor. Essas técnicas vão desde minificar os nossos arquivos CSS e JS (coisinha básica!) até otimizar o TCP (eita! que isso meu deus?).

[Aqui](https://speakerdeck.com/bevacqua/high-performance-in-the-critical-path) a talk dele. Fortemente recomendada para quem quiser ver algo que perdeu ou não foi no evento.

## Palestra 9 - Nick Desaulniers - Improving game performance on the Web: WASM, SharedArrayBuffer, SIMD, WebGL2

O Nick falou sobre o Web VR, a API para gerar realidades virtuais na Web.
Ele comentou sobre alguns pontos que o Damian já havia discutido na talk dele como Web Workers, SIDM, postMessage, SharedArrayBuffer e todas essas coisas que eu não conheco e estou pensando em estudar assim que digito isso.
Ele até nos desafiou a criar alguma coisa usando o Web VR para ganharmos uma camiseta hoje (22/08), no segundo dia do evento. (sim, estou fazendo isso depois da meia-noite). [Toma aí o link](http://nickdesaulniers.github.io/joshVR/).

## Palestra 10 - David Bryant - Keynote

Keynote sensacional com o "leader of the platform engineering team for Mozilla", ou como ele se auto-intitula "Web Platform guy".

Assim como o talk do Nicolas acho injusto tentar resumir a talk dele aqui pois ele comentou sobre bastante coisa, incluindo o Web VR, Web Assembly, WebRTC, Service Workers (offline capability, traffic interception) e coisas mais baixo nível como o JIT Coach.

Bom, é isso!

Após o segundo dia de evento pretendo complementar um pouco as informações postadas para deixar tudo mais completo, portanto continue acompanhando este link.

Qualquer coisa é só comentar aqui embaixo e compartilhar o conteúdo caso quiser.

Abraços!