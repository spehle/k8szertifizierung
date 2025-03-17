# Aufgabe 1

Erstelle einen Pod und eine ConfigMap

| Eigenschaft | Wert |
| --- | --- |
| Namespace | waterdeep |
| Name des Pods | nginx |
| Image | nginx:1.27.4-alpine |
| Name der ConfigMap | nginx-config-html |
| Name der Datei für die ConfigMap | nginx-content.html |
| Pfad für den VolumeMount | /usr/share/nginx/html |

## Lösung

1. Den Namespace erstellen.
Da der Namespace noch nicht existiert, muss er zuerst erstellt werden mit:

~~~
k create ns waterdeep
~~~

2. Die ConfigMap erstellen.
Die Datei mit dem Inhalt der ConfigMap liegt mit dem Namen nginx-content.html im Aufgabenverzeichnis.

~~~
k create -n waterdeep configmap nginx-config-html --from-file=index.html=nginx-content.html
~~~

Alternativ kann auch erst das yaml erzeugt und dann damit die ConfigMap erzeugt werden.

~~~
k create -n waterdeep configmap nginx-config-html --from-file=content=nginx-content.html --dry-run=client -oyaml > nginx-config-html.yaml
~~~

3. Die ConfigMap im Pod einbinden. Dazu erstellen wir erstmal eine yaml-Datei für den Pod.

~~~
k run -n waterdeep nginx --image=nginx:1.27.4-alpine --dry-run=client -oyaml > pod_nginx.yaml
~~~

Nun müssen wir im Pod die ConfigMap mounten. Dazu brauchen wir ein Volume. Dies wird auf der selben Höhe wie der Container erstellt. Dann brauchen wir im Container den VolumeMount. Das sollte folgendermassen aussehen.

~~~
 containers:
    ...
    volumeMounts:
    - name: content
      mountPath: /usr/share/nginx/html
      readOnly: true
    ...
  volumes:
  - name: content
    configMap:
      name: nginx-config-html
    ...
~~~

4. Kontrollieren ob die ConfigMap korrekt eingebunden wurde.

~~~
k -n waterdeep exec nginx -- curl localhost
~~~
