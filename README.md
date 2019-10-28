# Kit de integração Rede Vistorias

Como forma de integrar os serviços da Rede Vistorias com parceiros externos, criamos um kit com diferentes meios de realizar a integração, possibilitando ao parceiro selecionar o que melhor se adapta ao seu caso de uso.

## Formulario web

É a versão mais simplificada de integração, permitindo que o parceiro faça a integração com a Rede Vistorias com poucas alterações em seu software. 


- **Design pronto e customizável.** Fornecemos um formulário com design e front-end prontos para uso, dessa forma você não se preocupa com esses detalhes.
- **Não se preocupe com o fluxo.** Nós cuidamos de todo o fluxo do pedido, você só deve adicionar nosso código no seu front-end. 
- **Atualizações automáticas.** Seus usuário sempre terão acesso as atualizações assim que forem disponibilizadas, não havendo a necessidade de alterações no seu software. Além disso os usuário terão acesso ao fruto de um processo contínuo de aperfeiçoamento.

### Como usar?

- Inserir o código javascript em qualquer lugar dentro da tag `<body>`;
- Adicionar uma tag em qualquer lugar do seu código com um ID único;
- Setar o nome do parceiro com o método `rv('partner', '<PARTNER-NAME>')`;
- Especificar o tipo do pedido `rv('orderType', '<ORDER-TYPE>')`; (Opcional)
- Setar o CPF/CNPJ (com pontuação) `rv('document', '<DOCUMENT>')`; (Opcional)
- Especificar o vistoriador `rv('inspector', '{ name: <NAME>, email: <EMAIL> }')`; (Opcional)
- Especificar os serviços `rv('services', '[{ service: <SERVICE-NAME>, email: <RESPONSIBLE-EMAIL> }, ...]')`; (Opcional)

- Caso queira, poderá setar um callback para alguns eventos com o método `rv('on', '<EVENT>', function(parameters) { /* ... */ })`; (Opcional)
- Inicializar usando o ID do elemento adicionado no passo 2 com o método `rv('init')`

#### Exemplos
- Criando um pedido de vistoria
```
        <!-- ... -->
        <div id="sdk-rv"></div>
        <!-- ... -->
        <script>
            !function(r,v,s,d,k,i,n){
            if(r.rv)return;k=r.rv=function(){k.queue.push(arguments)};
            k.queue=[];i=v.createElement(s);i.async=!0;i.src=d;
            n=v.getElementsByTagName(s)[0];n.parentNode.insertBefore(i,n)
            }(window,document,'script','https://integration.redevistorias.com.br/js/app.js');
            rv('partner', 'Parceiro');
            rv('document', '111.111.111-11');
            rv('orderType', 'entrada');
            rv('on', 'order.created', function(code, price) { /* ... */ });
            rv('init', 'sdk-rv');
        </script>
    </body>
</html>
```
- Criando uma vistoria de checkout
```
        <!-- ... -->
        <div id="sdk-rv"></div>
        <!-- ... -->
        <script>
            !function(r,v,s,d,k,i,n){
            if(r.rv)return;k=r.rv=function(){k.queue.push(arguments)};
            k.queue=[];i=v.createElement(s);i.async=!0;i.src=d;
            n=v.getElementsByTagName(s)[0];n.parentNode.insertBefore(i,n)
            }(window,document,'script','https://integration.redevistorias.com.br/js/app.js');
            rv('partner', 'Parceiro');
            rv('document', '111.111.111-11');
            rv('orderType', 'checkout');
            rv('inspector', {
                'name': 'Jorge da Silva',
                'email': 'email@exemplo.com',
            });
            rv('services', [
                {
                    'service': 'Encanador',
                    'email': 'encanador@exemplo.com',
                },
                {
                    'service': 'Faxina',
                    'email': 'faxina@exemplo.com',
                }
            ]);
            rv('on', 'order.created', function(page_url) { /* ... */ });
            rv('init', 'sdk-rv');
        </script>
    </body>
</html>
```

### Eventos
| Tipo do pedido | Eventos | Parâmetros | Descrição |
|---|---|---|---|
| checkout | order.created | `page_url: String` | URL assinada para acesso ao aplicativo para a realização da vistoria.
| Demais tipos | order.created | `code: String`<br>`price: String` | Executado após a criação de um pedido.

---
## Zapier

Também possibilitamos a integração pelo Zapier. Com essa integração, o cliente pode solicitar vistorias utilizando um zap que irá enviar as informações para o zap da Rede Vistorias. Essa integração é focada em usuários que já são clientes da Rede Vistorias e possuem uma API Key válida (que pode ser gerada no seu painel de cliente). Além de conseguir solicitar as vistorias pelas actions do zapier, também é possível receber os retornos via triggers

Essa integração é particularmente interessante quando o cliente já utiliza algum aplicativo que tenha integração com o zapier (ex. pipedrive).

---
## API
Como forma de integração mais avançada, disponibilizamos uma API que o parceiro pode utilizar para cadastrar cliente e solicitar vistorias. Esta forma de integração permite mais liberdade para personalizar a experiência dos seus usuários, inclusive o fluxo e o design. Porém utilizando essa forma de integração, o parceiro precisará seguir a evolução da API com relação à novas versões quando forem lançadas, ou seja, deverá atualizar sua aplicação cada vez que uma nova funcionalidade for disponibilizada pela Rede Vistorias.

Mais detalhes sobre nossa API, e como funciona essa integração, podem ser encontrados na nossa documentação online em [http://docs.redevistorias.com.br/](http://docs.redevistorias.com.br/)
