# helm-chart-cisco-aci-tig-stack
Cisco ACI Monitor

Helm Chart based application for Cisco ACI monitoring with TIG Stack (Telegraf, InfluxDB, and Grafana).

## Usage

1. Install [Helm](https://helm.sh). For more information, see [Helm documentation](https://helm.sh/docs/).

2. Add the InfluxData Helm repository to download InfluxDB. Note that Telegraf and Grafana are locally in the project, so do not need to be downloaded:

   ```console
   helm repo add influxdata https://helm.influxdata.com/
   ```
   
3. Build the Helm Chart dependencies:

   ```console
   helm dependency build .
   ```

4. Update the Telegraf values in **values.yaml** with your APIC informations:

   ```console
   telegraf-apic1:
     env:
       - name: APIC_ADDRESS
         value: <apic-url>
       - name: APIC_USER
         value: <apic-username>
       - name: APIC_PASSWORD
         value: <apic-password>
   ```

5. Update the InfluxDB URL in **values.yaml**, by default it is set in a namespace named "monitor":

   ```console
   http://apps-influxdb.<namespace>:8086
   ```
   
6. Build the application:

   ```console
   helm install apps . -n <namespace>
   ```

7. Allows the user to access and interact with internal Kubernetes cluster processes from your localhost:

   ```console
   kubectl port-forward service/apps-grafana 3000:80 -n <namespace>
   ```
