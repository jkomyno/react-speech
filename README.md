****************************************
ReactJS: un'interfaccia JavaScript dedicata alle interfacce utente
****************************************

ReactJs è una libreria javascript per costruire *UI* composte da **componenti riutilizzabili**. React si dedica principalmente alla View, ovvero la parte di un qualsiasi progetto che si occupa di visualizzare i contenuti della logica di software (model) e di regolare l'interazione tra utenti e servizi. 

Grazie all'utilizzo di *JSX*, un dialetto del JavaScript, è possibile definire la struttura di ogni componente, che sarà composto di:
* **DOM**: struttura logica di rappresentazione sulla pagina web
* **Comportamento**: come l'applicazione reagisce alle azioni che compie l'utente

Ogni componente React tiene rigorosamente conto di ogni suo **stato**. Gli stati del componente corrispondono alle variabili che ogni suo oggetto assume al momento della creazione.
Il punto cruciale della visualizzazione di un componente è il metodo *render()*: vediamone un esempio.

.. code-block:: javascript

	var HelloMessage = React.createClass({
	  render: function() {
		return <div>Hello {this.props.name}</div>;
	  }
	});