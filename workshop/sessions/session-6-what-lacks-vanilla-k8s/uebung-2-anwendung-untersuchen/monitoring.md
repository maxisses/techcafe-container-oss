# Monitoring

In this exercise, we'll explore the out-of-the-box logging and monitoring capabilities that are offered in OpenShift.

## Simulate Load on the Application

1. ```bash
    while sleep 1; do curl -s http://<host>/productpage; done
   ```

   With Windows:

   ```bash
    while($true){curl http://<host>/productpage}
   ```

## --&gt; metrics auf pod level \( cpu / memory

--&gt; monitoring sicht per projekt mit dashboard metrics events

