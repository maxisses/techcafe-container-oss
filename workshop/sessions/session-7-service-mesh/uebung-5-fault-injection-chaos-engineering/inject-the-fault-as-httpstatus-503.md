# Inject the fault as httpStatus 503

```text
http:
    - fault:
        abort:
          httpStatus: 503
          percentage:
            value: 50
```



```text
http:
    - fault:
        abort:
          httpStatus: 418
          percentage:
            value: 50
```

