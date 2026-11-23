# Sankofa Media

Open multimedia projects about culture, built in the open and published under
Apache 2.0. Every project is a website you can read, a codebase you can run, and
a place where you can fix, add or suggest a story.

Русская версия: [README.ru.md](README.ru.md).

## Projects

### [Sankofa](https://github.com/sankofa-media/sankofa) — [sankofa.black](https://sankofa.black/)

A museum of seven centuries of Black culture, from the libraries of Timbuktu to
the starships of Sun Ra, in English and Russian. Short cards tied to a place and
a year, each backed by a primary source or two independent ones; an atlas, a
timeline, roots of artists, a workshop of musical elements, and long special
projects told scene by scene with sound.

It is also a Kubernetes distribution, and the museum ships inside it (see below).

Special projects: [Sea Lion Girls](https://sankofa.black/features/sea-lion-girls/),
[Forever Changes](https://sankofa.black/features/forever-changes/),
[Angel](https://sankofa.black/features/angel/) — all of them in
[English](https://sankofa.black/features/) and [Russian](https://sankofa.black/ru/features/).

### Sankofa as a Kubernetes distribution

Sankofa is a [kuberoot](https://github.com/kuberoot-dev/kuberoot) distribution
that passes upstream Kubernetes conformance, and its features also install as
add-ons on any cluster. Each one is named after the culture it comes from.

| Feature | What it gives a cluster |
|---|---|
| **Griot**, the memory | The life of every object, even after deletion: `sankofa tell deployment/web`, `kubectl get timelines`. Secret values are never stored; reading follows RBAC. |
| **Sankofa fetch** | Brings back one object or a whole namespace as it was at any moment, and diffs two moments: `sankofa fetch namespace/shop --at 2h`. |
| **Kgotla** | Protected objects are deleted only after a council: every named voice has spoken, the chief last. |
| **Polyrhythm** | `H` in a CronJob minute (`H 3 * * *`) spreads jobs across free beats instead of starting them all at once. |
| **Credits** | Walks an image's declared lineage; a webhook warns about or refuses images that hide their base, source or licence. |
| **Story** | Tells an incident in three books (events, changes, heirs) and shows where they disagree. |
| **Pulse** | The cluster's heartbeat as a live stream; the museum plays it as drums. |

For a person at the terminal: `sankofa dict`, an endless dictionary in the
manner of Pavić; `sankofa atlas`, a braille world map with a timeline;
`sankofa genre`, music as a dependency graph; `sankofa quest`, real dilemmas
and quizzes. Details: the
[Sankofa README](https://github.com/sankofa-media/sankofa#what-it-does-for-a-cluster).

### [Dormer](https://github.com/sankofa-media/dormer) — [dormer.sankofa.workshop.aenix.io](https://dormer.sankofa.workshop.aenix.io/)

Independent multimedia stories about music and art, on any subject, in English
and Russian. Built on the same scene engine as Sankofa's special projects.

## Run them yourself

**The Sankofa museum, locally** (needs Docker), then open <http://localhost:8080>:

```sh
git clone https://github.com/sankofa-media/sankofa && cd sankofa
docker build -f web/Dockerfile --build-arg SITE_URL=http://localhost:8080 -t sankofa-museum .
docker run --rm -p 8080:8080 sankofa-museum
```

On your own domain or in Kubernetes: set `SITE_URL` to your origin and follow
[docs/self-host.md](https://github.com/sankofa-media/sankofa/blob/main/docs/self-host.md)
(`deploy/museum.yaml`, optional TLS and a second host). The optional Angel
service (shared words, the pulse) is described in `deploy/angel.yaml`; the
museum works without it.

**The Sankofa distribution features on any cluster:**

```sh
kubectl apply -f deploy/crds/
kubectl apply -f deploy/griot.yaml      # set the Griot image in it first
kubectl apply -f deploy/webhooks.yaml
go install github.com/sankofa-media/sankofa/cmd/sankofa@latest
```

The full kuberoot distribution (signed node images, A/B upgrades, passes upstream
Kubernetes conformance) is in
[docs/kuberoot.md](https://github.com/sankofa-media/sankofa/blob/main/docs/kuberoot.md).

**Dormer, locally** (needs Node 24+), then open <http://localhost:4173>:

```sh
git clone https://github.com/sankofa-media/dormer && cd dormer
npm ci && npm run build && npm run preview
```

## Take part

- **Fix or suggest something** without any code: use the "Suggest or correct"
  button at the bottom of any page on [sankofa.black](https://sankofa.black/), or
  [open an issue](https://github.com/sankofa-media/sankofa/issues/new/choose):
  a correction, an idea for a special project, a topic you want explained, a new
  dictionary card.
- **Write or change something yourself**: read
  [CONTRIBUTING.md](https://github.com/sankofa-media/.github/blob/main/CONTRIBUTING.md)
  and open a pull request.

Everything here is free to read, run, fork and reuse under the Apache License 2.0.
