#  Coverage: The Essential Coverage Reporter GitHub Action

> Parse and publish coverage xml to a PR, enforce coverage rate on new & modified files

## Usage

Create a new workflow `.yml` file in the `.github/workflows/` directory.

You can create a coverage report:
 - pytest `$ pytest --cov-report xml:path/to/coverage.xml`
 - coverage `$ coverage xml path/to/coverage.xml`
 - jest `$ jest --coverage --coverageReporters="text" --coverageReporters="cobertura"`

### Minimal Configuration
```yml
name: 'coverage'
on:
    pull_request:
        branches:
            - master
            - main
jobs:
    coverage:
        runs-on: ubuntu-latest
        steps:
          - name: Run tests
            run: npm run test -- --coverage --coverageReporters="text" --coverageReporters="cobertura"
          - name: Coverage Report for Changed Files
            uses: zimosworld/coverage@v1.0
            with:
              coverageFile: ./coverage/cobertura-coverage.xml
              token: ${{ secrets.GITHUB_TOKEN }}
              thresholdAll: 0
              thresholdNew: 0
              thresholdModified: 0
```

## Inputs

| Input                           | Optional | Description                                           | Default Value              | Example                       |
|---------------------------------|----------|-------------------------------------------------------|----------------------------|-------------------------------|
| `coverageFile`                  |          | Path to cobertura .xml coverage report                |                            | ./path/to/coverage.xml        |
| `token`                         |          | Github token                                          |                            | ${{ secrets.GITHUB_TOKEN }}   |
| `thresholdAll`                  |          | Minimal average line coverage                         |                            | 0.8                           |
| `thresholdNew`                  |          | Minimal average new files line coverage               |                            | 0.9                           |
| `thresholdModified`             |          | Minimal average modified files line coverage          |                            | 0.0                           |
| `passIcon`                      | ✅        | Indicator for files that passed                       | 🟢                         | 🟢                            |
| `failIcon`                      | ✅        | Indicator for files that failed                       | 🔴                         | 🔴                            |
| `sourceDir`                     | ✅        | Directory to use as the source of the coverage report | /                          | ./path/to/src                 |
| `commentTitle`                  | ✅        | Title of the comment added to the PR                  | Pull Request Code Coverage |                               |
| `shouldCountRenamedAsModified ` | ✅        | Switch to count renamed files as modified             | true                       |                               |

