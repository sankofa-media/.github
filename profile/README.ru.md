# Sankofa Media

Открытые мультимедийные проекты о культуре. Всё делается открыто и
публикуется под лицензией Apache 2.0. Каждый проект — это сайт, который можно
читать, код, который можно запустить у себя, и место, где можно поправить,
дополнить или предложить историю.

English version: [README.md](README.md).

## Проекты

### [Sankofa](https://github.com/sankofa-media/sankofa) — [sankofa.black](https://sankofa.black/ru/)

Музей семи веков чёрной культуры, от библиотек Тимбукту до звездолётов Сан Ра,
на русском и английском. Короткие карточки с местом и годом, и за каждой —
первоисточник или два независимых источника. Атлас, лента времени, корни
исполнителей, мастерская музыкальных элементов и большие спецпроекты, которые
рассказываются сцена за сценой, со звуком.

Это ещё и дистрибутив Kubernetes, и музей едет внутри него (см. ниже).

Спецпроекты: [Sea Lion Girls](https://sankofa.black/ru/features/sea-lion-girls/),
[Forever Changes](https://sankofa.black/ru/features/forever-changes/),
[Angel](https://sankofa.black/ru/features/angel/) — все
[на русском](https://sankofa.black/ru/features/) и
[на английском](https://sankofa.black/features/).

### Sankofa как дистрибутив Kubernetes

Sankofa — дистрибутив на [kuberoot](https://github.com/kuberoot-dev/kuberoot),
который проходит проверку соответствия Kubernetes, а его возможности ставятся
и как дополнения на любой кластер. Каждая названа по той культуре, из которой
взята.

| Возможность | Что она даёт кластеру |
|---|---|
| **Griot**, память | Жизнь каждого объекта, даже после удаления: `sankofa tell deployment/web`, `kubectl get timelines`. Значения секретов не хранятся, чтение подчиняется RBAC. |
| **Sankofa fetch** | Возвращает объект или целое пространство имён таким, каким оно было в любой момент, и сравнивает два момента: `sankofa fetch namespace/shop --at 2h`. |
| **Kgotla** | Защищённый объект удаляется только после совета: высказались все названные голоса, вождь — последним. |
| **Polyrhythm** | `H` в минутах CronJob (`H 3 * * *`) разносит задания по свободным долям, чтобы они не стартовали разом. |
| **Credits** | Проходит по заявленной родословной образа; вебхук предупреждает или не пускает образы, которые скрывают основу, исходники или лицензию. |
| **Story** | Рассказывает об инциденте в трёх книгах (события, изменения, наследники) и показывает, где они расходятся. |
| **Pulse** | Сердцебиение кластера в живом потоке; музей играет его как барабаны. |

Для человека в терминале: `sankofa dict` — бесконечный словарь в духе Павича;
`sankofa atlas` — карта мира шрифтом Брайля с лентой времени; `sankofa genre` —
музыка как граф зависимостей; `sankofa quest` — настоящие дилеммы и викторины.
Подробности — в [README Sankofa](https://github.com/sankofa-media/sankofa/blob/main/README.ru.md).

### [Dormer](https://github.com/sankofa-media/dormer) — [dormer.sankofa.workshop.aenix.io](https://dormer.sankofa.workshop.aenix.io/ru/)

Независимые мультимедийные истории о музыке и искусстве, на любые темы, на
русском и английском. Работают на том же движке сцен, что и спецпроекты Sankofa.

## Как запустить у себя

**Музей Sankofa на своём компьютере** (нужен Docker), потом откройте
<http://localhost:8080>:

```sh
git clone https://github.com/sankofa-media/sankofa && cd sankofa
docker build -f web/Dockerfile --build-arg SITE_URL=http://localhost:8080 -t sankofa-museum .
docker run --rm -p 8080:8080 sankofa-museum
```

На своём домене или в Kubernetes: укажите свой адрес в `SITE_URL` и следуйте
[docs/self-host.md](https://github.com/sankofa-media/sankofa/blob/main/docs/self-host.md)
(`deploy/museum.yaml`, TLS и второй домен по желанию). Необязательный сервис
Angel (общие слова и пульс) описан в `deploy/angel.yaml`; музей работает и без
него.

**Возможности дистрибутива Sankofa на любом кластере:**

```sh
kubectl apply -f deploy/crds/
kubectl apply -f deploy/griot.yaml      # сначала укажите в нём образ Griot
kubectl apply -f deploy/webhooks.yaml
go install github.com/sankofa-media/sankofa/cmd/sankofa@latest
```

Полный дистрибутив на kuberoot (подписанные образы узлов, обновление A/B,
проходит проверку соответствия Kubernetes) описан в
[docs/kuberoot.md](https://github.com/sankofa-media/sankofa/blob/main/docs/kuberoot.md).

**Dormer на своём компьютере** (нужен Node 24+), потом откройте
<http://localhost:4173>:

```sh
git clone https://github.com/sankofa-media/dormer && cd dormer
npm ci && npm run build && npm run preview
```

## Как участвовать

- **Поправить или предложить без кода:** нажмите «Предложить или поправить»
  внизу любой страницы на [sankofa.black](https://sankofa.black/ru/) или
  [заведите задачу](https://github.com/sankofa-media/sankofa/issues/new/choose):
  поправка, идея спецпроекта, тема, которую стоит разобрать, новая словарная
  карточка.
- **Написать или изменить самому:** прочитайте
  [CONTRIBUTING.ru.md](https://github.com/sankofa-media/.github/blob/main/CONTRIBUTING.ru.md)
  и откройте pull request.

Всё здесь можно свободно читать, запускать, форкать и использовать по лицензии
Apache 2.0.
