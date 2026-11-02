# K6 lab

Performance testing lab for ITDS362 using Grafana K6 and QuickPizza.

## Setup

- Install K6 and check with `k6 version`.
- Run the commands below from this folder.
- The tests were run with K6 v2.2.0.

## Part 0

```powershell
k6 run 01-first-test.js
k6 run --vus 5 --duration 20s 01-first-test.js
k6 run --vus 5 --iterations 20 01-first-test.js
k6 run 04-pizza-api.js
k6 run 05-no-token.js
k6 run 06-thresholds.js
$LASTEXITCODE
k6 run -e P95=300 06-thresholds.js
$LASTEXITCODE
k6 run 07-requirement.js
$LASTEXITCODE
k6 run -e P95=1 07-requirement.js
$LASTEXITCODE
k6 run explore.js
k6 run --vus 5 --duration 20s 08-bug-hunt.js
```

`08-bug-hunt.js` contains the fixed request. The original problem and the results before and after the fix are explained in `RESULTS.md`.

## Part A

Run one test at a time. All five tests use `journey.js`.

```powershell
k6 run a1-smoke.js
k6 run --out web-dashboard=export=reports/a2-average.html a2-average.js
k6 run --out web-dashboard=export=reports/a3-stress.html a3-stress.js
k6 run --out web-dashboard=export=reports/a4-spike.html a4-spike.js
k6 run --out web-dashboard=export=reports/a5-soak.html a5-soak.js
```

Open the HTML files in `reports` to view the charts. Measurements and answers are in `RESULTS.md`.

The largest test uses 5 virtual users. The soak test uses 2 users, with 30 seconds to ramp up, 10 minutes at 2 users, and 30 seconds to ramp down.
