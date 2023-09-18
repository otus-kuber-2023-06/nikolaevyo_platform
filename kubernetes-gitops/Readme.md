Создание кластера 
https://gitlab.com/nikolaevyo/k8s-cluster

Сборка и пуш
https://gitlab.com/nikolaevyo/microservices-demo

Видим новый ревижен хелм чарта для деплоя
"level":"info","ts":"2023-09-11T19:45:25.972Z","msg":"artifact up-to-date with remote revision: '0.21.0+d812d1454c88'","controller":"helmchart","controllerGroup":"source.toolkit. │

Ставить через Istio operator не стал, т.к. 
Use of the operator for new Istio installations is discouraged in favor of the Istioctl and Helm installation methods. While the operator will continue to be supported, new feature requests will not be prioritized.

Релиз был не успешен из за отсуствия трафика, а ещё к истио нужно было подключить плагин прометеуса, а ещё имя гейтвея указано было не верно т.к. он в другом неймспейсе



│   Normal   Synced  22m                  flagger  New revision detected! Scaling up frontend.microservices-demo                                                                                           │
│   Normal   Synced  20m                  flagger  Starting canary analysis for frontend.microservices-demo                                                                                                │
│   Normal   Synced  20m                  flagger  Advance frontend.microservices-demo canary weight 5                                                                                                     │
│   Normal   Synced  18m                  flagger  Advance frontend.microservices-demo canary weight 10                                                                                                    │
│   Normal   Synced  16m                  flagger  Advance frontend.microservices-demo canary weight 15                                                                                                    │
│   Normal   Synced  14m                  flagger  Advance frontend.microservices-demo canary weight 20                                                                                                    │
│   Normal   Synced  12m                  flagger  Advance frontend.microservices-demo canary weight 25                                                                                                    │
│   Normal   Synced  8m34s                flagger  Advance frontend.microservices-demo canary weight 30                                                                                                    │
│   Warning  Synced  6m34s (x2 over 10m)  flagger  Halt advancement no values found for istio metric request-success-rate probably frontend.microservices-demo is not receiving traffic: running query fai │
│ led: no values found                                                                                                                                                                                     │
│   Normal   Synced  4m34s                flagger  Copying frontend.microservices-demo template spec to frontend-primary.microservices-demo                                                                │
│   Normal   Synced  34s (x2 over 2m34s)  flagger  (combined from similar events): Promotion completed! Scaling down frontend.microservices-demo           



NAME       STATUS      WEIGHT   LASTTRANSITIONTIME
frontend   Succeeded   0        2023-09-14T17:51:56Z
