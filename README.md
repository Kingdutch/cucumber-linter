<h1 align="center">Cucumber Linter - Static analysis tool for Cucumber and Behat</h1>

------

Cucumber Linter focuses on providing consistent formatting for Cucumber (.feature) files.

## Getting Started
Cucumber Linter requires PHP >= 8.0 to function. The linter expects your files to have the 
`.feature` extension.

### Installation
To start linting your Cucumber/Gherkin files, require Cucumebr Linter using [Composer](https://getcomposer.org/).

```bash
composer require --dev kingutch/cucumber-linter
```

Composer will install Cucumber Linter’s executable in its `bin-dir` which defaults to `vendor/bin`.

You can also download the [latest PHAR](https://github.com/kingdutch/cucumber-linter/releases) and 
just use that.

### Running the linter
To lint your test files, point the linter to the right file(s) or directory.

For example to lint your `checkout` and `login` Behat files:
```bash
vendor/bin/cucumber-linter tests/behat/features/capabilities/checkout tests/behat/features/capabilities/login
```

## Rules enforced
In this initial release the linter does not provide a way to configure which rules are running 
or add rules, but has a hardcoded list of rules.

Current rules are aimed at writing focused and consistent tests that clearly test a single thing.
Tests should go through the three stages of `arrange`, `act`, `assert`. In the `arrange` stage 
pre-required existing (tested elsewhere) functionality is scaffolded. In the `act` stage we're 
taking some user action that triggers business logic. In the `assert` state we verify that the 
result of the action with the business logic has the desired result.

Scenarios should be written in such a way that the different stages of a test are easily 
identifyable. Additionally each stage should only occur once. A repetition of a stage suggests 
the test may be unfocused and should be split into multiple scenarios. Keeping scenario's 
focused on testing a limited scope provides stakeholders with the most information when they 
fail and reduces the scope of work that requires debugging to find a cause.

### Requires backgrounds to be non-empty
Empty `background`s will not cause errors in test executors but they create visual noise for 
people reading the test and it provides unclarity over the test writer's intentions.

### Requires the first step in a background to be Given
Backgrounds provide shared scaffolding so they should always be an extension of the `arrange` 
phase, hence `Given`.

### Requires subsequent steps in a background to start with And
Backgrounds provide shared scaffolding so they should always be an extension of the `arrange`
phase, so subsequent steps to the first one are part of the same stage denoted by `And`.

### Requires indentation within backgrounds and scenario's to be constant
This ensures there's a consistent left indentation for the eye to jump back to when reading the 
test file as test.

### Requires a blank line before When and Then blocks
This provides the visual separation between the different phases in a test allowing for easy 
scannability.

### Requires the first step in a scenario to be Given
The first step in a test should be to `arrange` the system into a known working state, this is 
signaled by `Given`. 

### Requires Given, When, and Then to occur exactly once in a scenario in order
Repetition of words signalling a certain stage indicate that a scenario should probably be split 
up. Enforcing the `Given`, `When`, and `Then` order enforces the `arrange`, `act`, and `assert` 
order of the scenario. 

## Contributing

Any contributions are welcome. Cucumber Linter's source code open to pull requests lives at [`kingdutch/cucumber-linter-src`](https://github.com/kingdutch/cucumber-linter-src).
