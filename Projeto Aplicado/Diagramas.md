https://colab.research.google.com/drive/1HFNup6hsPtCMYuEKKjAHrKDRxiLjLJh7?usp=sharing

#python #diagram #draw

```python
!pip install diagrams
from diagrams import Diagram, Cluster

graph_attr = {
"bgcolor": "transparent"
}

from diagrams.onprem.client import Users
from diagrams.oci.storage import StorageGateway as st
from diagrams.oci.network import LoadBalancer as lb
from diagrams.oci.compute import OKE
from diagrams.gcp.analytics import PubSub
from diagrams.onprem.network import Internet as Web

# filename="arch", outformat="jpg"
with Diagram("CVM Reader", show=False, graph_attr=graph_attr, filename="arch", outformat="jpg") as diag:
	user = Users("Multiple Users")

	with Cluster("Kubernets"):

		ep = lb("LoadBalancer")
		api = OKE("API")
		msg = PubSub("Mensageria")
		cvm = Web("Site CVM")

		with Cluster("Fila"):
			queue = [OKE("Assinante1"),
			OKE("Assinante1"),
			OKE("AssinanteN")]
			
		with Cluster("Banco de Dados"):
			db = st("Database")
			db - [st("Database replica")]

	user >> ep >> api >> msg >> queue >> cvm
	queue >> db
diag

```

![[arch.jpg]]