# Aufgabe 2

Nutze die bereits vorhandene ConfigMap und das vorhandene Pod.
Ergänze das Pod um ein Secret mit drei Werten die du als Umgebungsvariablen in dem Pod einbindest
Erstelle einen Service der das Pod vom Host aus erreichbar macht.

| Eigenschaft | Wert |
| --- | --- |
| Namespace | waterdeep |
| Name des Pods | nginx |
| Image | nginx:1.27.4-alpine |
| Name der ConfigMap | nginx-config-html |
| Name der Datei für die ConfigMap | nginx-content.html |
| Pfad für den VolumeMount | /usr/share/nginx/html |
| **Name des Secrets** | nginx-secret |
| Inhalt des Secrets | nginx_user=nginx |
| | nginx_password=SuperGeheimesPasswort123! |
| | nginx_http_port=9090 |
