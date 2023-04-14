# Example deployment of Homu

What is Homu: <https://bors.tech/homu-io/>

[Rust’s fork](https://github.com/rust-lang/homu) is the most maintained,
though [Servo’s fork](https://github.com/servo/homu) has also evolved separately
and got a few features (such as dry-running a selected subset of CI with “try choosers”).

Fly.io’s free allowance looks more than enough for hosting Homu:
<https://fly.io/docs/about/pricing/#free-allowances>

## Repository layout

* `rust-lang-homu` is a git submodule
* `Dockerfile`, `homu`, and `setup.py` are symbolic links into it
  so that a different `cfg.production.toml` can be used without forking that repo
* `cfg.production.toml` and `fly.toml` are “local” configuration

## Setup

1. Configure `cfg.production.toml`
2. Create a new Fly app: <https://fly.io/docs/speedrun/>
3. Add a persistent volume: `flyctl volumes create --region $REGION --size 1 data`,
   make sure `fly.toml` has corresponding config.
4. Add secret tokens: `flyctl secrets import`
   (I prefer this over `flyctl secrets set` so they don’t stick around in shell history)

   ```
   GH_ACCESS_TOKEN=…
   APP_CLIENT_ID=…
   APP_CLIENT_SECRET=…
   ^D
   ```
