### Kubernetes GateWay
*[K8s api docs](https://gateway-api.sigs.k8s.io/reference/api-types/gateway/)*

The Kubernetes gateway in simple terms, it's a component in k8s whcih handles and controls traffic.

The Gateway is made up of 3 subcomponents that make it work
	- __The GateWay class__
		This defines the controller class that the gateway will make use of, as well as defining the gateway's name
	
	- __The Gateway__
		For this one, I l'd love to relate it to OOP, the gateway is the actual class, the instance of the gateway class. This gateway can be of any defined GatewayClass. This is where you will define your listeners(Listen for traffic and transfer the traffic). These gateway objects typically handle one or more listeners.
		Listeners describe how the gateway should listen for traffic and has a port, protocal and other protocol specific details.
		The traffic that flows in the API must match a single listener.
		It is also a load-balancer

	- __Routes__ 
		To keep it simple, these define how traffic is routed to services.




