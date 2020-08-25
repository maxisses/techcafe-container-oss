# simplen Health Check einbauen

**Health check einbauen - lokal**

* startet eure anwendung mit npm run start 
* geht dann im browser auf: localhost:3000/health- dort seht ihr ein "json" {status: up}- öffnet danach den ordner test/functional und die datei "test-routes.js"- dies ist eine datei die alle pfade eurer App prüft, wenn ihr eure App ändert müssen auch die Tests angepasst werden

**Health check einbauen - in der Delivery Pipeline**

* navigiere in die Delivery Pipeline wo jetzt hoffentlich alles grün ist und deine app unter 

```text
https://staging-Domain eurer App/
https://Domain eurer App/
```

![](../../.gitbook/assets/image%20%2824%29.png)

- Clicke auf "Add Stage" rechts oben, ersetze MyStage durch "Health Check"

- Clicke auf Jobs - Add Job - Test

- füge folgendes in das Test Script Feld ein, ersetzt die URL eurer applikation:

```text
export appstatus=`curl -s 'https://staging-<eure url>/health' |     python3 -c "import sys, json; print(json.load(sys.stdin)['status'])"`
if [[ "$appstatus" == "UP" ]]; then 
   echo "App is Up"
   exit 0
else
   echo "App could not be reached"
   exit 1
fi
```

--&gt; Save nicht vergessen und die Stage dann zwischen Deploy to Staging und Deploy to Prod schieben--&gt; ausführen indem ihr auf play drückt oder die ganze Pipeline neu anstoßt

