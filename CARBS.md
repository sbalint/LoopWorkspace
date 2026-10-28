# Carbs integration branch

`carbs-next-dev` is LoopKit's `next-dev` plus the changes that let Loop offer meals logged in
[Carbs](https://github.com/sbalint/Carbs) as carb suggestions. Nothing is entered automatically:
every suggestion opens Loop's normal carb entry and bolus screens for you to confirm.

| Repo | Branch | Based on |
|---|---|---|
| sbalint/LoopWorkspace | `carbs-next-dev` | LoopKit/LoopWorkspace `next-dev` |
| sbalint/Loop (submodule `Loop`) | `carbs-next-dev` | the Loop commit LoopKit's `next-dev` pins |

All other submodules still come from LoopKit unchanged.

## Pulling in new next-dev changes

```bash
# Workspace
git fetch origin && git merge origin/next-dev
# Loop: move our branch onto the Loop commit next-dev now pins
NEW=$(git ls-tree origin/next-dev Loop | awk '{print $3}')
cd Loop && git fetch origin && git merge $NEW && git push sbalint carbs-next-dev && cd ..
git submodule update --init --recursive
git add Loop && git commit -m "Bump Loop to next-dev $NEW plus Carbs changes" && git push sbalint carbs-next-dev
```

Resolve any conflicts in the Carbs changes, build, and test with the simulated pump and CGM before
installing on a phone.
