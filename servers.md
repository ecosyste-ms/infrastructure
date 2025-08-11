# Services

| Service           | IP             | Requirements |
|-------------------|----------------|--------------|
| repos             | 195.154.87.126 | very high    |
| timeline          | 51.15.160.73   | very high    |
| packages db       | 195.154.29.88  | high         |
| packages web      | 51.15.23.142   | high         |
| parser            | 195.154.81.95  | high         |
| commits           | 195.154.29.100 | medium       |
| docker            | 62.210.217.62  | medium       |
| issues            | 51.159.56.73   | medium       |
| archives          | 51.159.31.55   | medium       |
| home              | 195.154.82.7   | low          |
| resolve           | 195.154.82.7   | low          |
| advisories        | 195.154.82.7   | low          |
| summary           | 195.154.82.7   | low          |
| conda-api         | 195.154.82.7   | low          |
| npm-update-stream | 195.154.82.7   | low          |
| blog              | 195.154.82.7   | low          |
| digest            | 195.154.82.7   | low          |
| diff              | 195.154.82.7   | low          |
| licenses          | 195.154.82.7   | low          |
| awesome           | 195.154.82.7   | low          |
| dashboard         | 195.154.82.7   | low          |
| dependabot        | 62.210.127.225 | low          |
| funds             | 195.154.82.7   | low          |
| opencollective    | 195.154.82.7   | low          |
| ost               | 195.154.82.7   | low          |
| papers            | 51.15.23.142   | low          |
| ruby              | 195.154.82.7   | low          |
| sbom              | 195.154.82.7   | low          |
| sponsors          | 195.154.82.7   | low          |

# Servers

| Server         | Number of Services | Size       | Distro |
|----------------|--------------------|------------|--------|
| 195.154.87.126 | 1 (repos)          | Very Large | Ubuntu 20.04.6 LTS |
| 51.15.160.73   | 1 (timeline)       | Very Large | Ubuntu 22.04.5 LTS |
| 51.15.23.142   | 2 (packages web, papers) | Large | Ubuntu 20.04.6 LTS |
| 195.154.29.88  | 1 (packages db)    | Large      | Ubuntu 20.04.6 LTS |
| 195.154.29.100 | 1 (commits)        | Large      | Ubuntu 20.04.6 LTS |
| 195.154.81.95  | 1 (parser)         | Large      | Ubuntu 20.04.6 LTS |
| 51.159.56.73   | 1 (issues)         | Large      | Ubuntu 24.04.2 LTS |
| 62.210.127.225 | 1 (dependabot)     | Medium     | Ubuntu 22.04.5 LTS |
| 62.210.217.62  | 1 (docker)         | Small      | Ubuntu 22.04.6 LTS |
| 195.154.82.7   | 18                 | Large      | Ubuntu 20.04.6 LTS |
| 51.159.31.55   | 1 (archives)       | Medium     | Ubuntu 22.04.5 LTS |
