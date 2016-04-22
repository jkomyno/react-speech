==================================================================
ReactJS: un'interfaccia JavaScript dedicata alle interfacce utente
==================================================================

**ReactJs** è una libreria javascript per costruire *UI* composte da **componenti riutilizzabili**. React si dedica principalmente alla View, ovvero la parte di un qualsiasi progetto che si occupa di visualizzare i contenuti della logica di software (model) e di regolare l'interazione tra utenti e servizi. 

Grazie all'utilizzo di *JSX*, un dialetto del JavaScript, è possibile definire la struttura di ogni componente, che sarà composto di:
* **DOM**: struttura logica di rappresentazione sulla pagina web
* **Comportamento**: come l'applicazione reagisce alle azioni che compie l'utente

=====================
Creatori e casi d'uso
=====================


Il punto cruciale della visualizzazione di un componente è il metodo *render()*: vediamone un esempio.

```javascript
	var HelloMessage = React.createClass({
	  render: function() {
		return <div>Hello {this.props.name}</div>;
	  }
	});
```

Ogni componente React tiene rigorosamente conto di ogni suo **stato**. Gli stati del componente corrispondono alle variabili che ogni suo oggetto assume al momento della creazione, e vengono dichiarati nel metodo *getInitialState()*.
Inoltre, è ovviamente supportato il salvataggio dell'input dell'utente, nelle cosiddette *props*, ovvero **Proprietà**, come vedremo in seguito.

```javascript
	var Timer = React.createClass({
	  getInitialState: function() {
	    // ritorna un oggetto
		return {secondsElapsed: 0};
	  },
	  // metodo custom per simulare il comportamento di un orologio, secondo dopo secondo
	  tick: function() {
		this.setState({secondsElapsed: this.state.secondsElapsed + 1});
	  },
	  componentDidMount: function() {
		this.interval = setInterval(this.tick, 1000);
	  },
	  componentWillUnmount: function() {
		clearInterval(this.interval);
	  },
	  render: function() {
		return (
		  <div>Seconds Elapsed: {this.state.secondsElapsed}</div>
		);
	  }
	});

ReactDOM.render(<Timer />, mountNode);
```

Andiamo subito ad analizzare il codice sopra riportato. Com'è possibile osservare, il componente Timer è composto da una particolare classe che contiene i metodi *getInitialState()*, *tick()*, *componentDidMount()*, *componentWillUnmount()* e *render()*.

* **getInitialState()**: Metodo invocato una volta sola, appena prima che il componente venga creato. Il valore ritornato sarà utilizzato come valore iniziale per *this.state*, il contenitore degli stati del componente.
* **componentDidMount()**: Metodo invocato una volta sola subito dopo il rendering iniziale del componente. Vale solo per il lato client (e non per il server). Da questo componente del ciclo di vita della View, è possibile accedere ad ogni riferimento (refs) dei componenti figli.
* **componentWillUnmount**: Invocato non appena si interrompe il rendering del componente. Esso compie ogni *pulizia* necessaria nella View, come ad esempio invalidare il timer precedente creato o eliminare ogni commento o like sotto ad un post, o comunque ogni cosa creata all'interno di componentDidMount().

=======================
Integrazione con jQuery
=======================

L'utilizzo di ReactJS come **View manager** per la nostra applicazione web ci lascia liberi di utilizzare altre librerie a cui magari ogni sviluppatore front end (ovvero di siti WEB) è abituato: il caso più eclatante è quello di jQuery.
Ecco un esempio che dimostra l'utilizzo di **AJAX** (Asynchronous Javascript And *XML*) all'interno di uno dei metodi di ReactJS precedentemente elencati:

```javascript
  componentDidMount: function() {
    $.ajax({
      url: this.props.url,
      dataType: 'json',
      cache: false,
      success: function(data) {
        this.setState({data: data});
      }.bind(this),
      error: function(xhr, status, err) {
        console.error(this.props.url, status, err.toString());
      }.bind(this)
    });
  },
```

AJAX è estremamente comodo quando si desidera **interagire con un server senza dover ricaricare la pagina** (come invece avviene in PHP): sarebbe inutile rinunciare a questa comodità e ricrearla ex novo ogni qualvolta fosse necessario!
*Approfondimenti su AJAX:* http://www.w3schools.com/jquery/jquery_ref_ajax.asp

================================
Spunti & Articoli di Terze Parti
================================

* http://reactfordesigners.com/labs/reactjs-introduction-for-people-who-know-just-enough-jquery-to-get-by/