# YAML

## cron jobs

```yml
schedules:
  - cron "0 10 * * *"
    displayName: "Daily 10am UTC (3am PST) build"
    branches:
      include:
        - main
```

## keep in mind

- container defs for different build systems
- security development lifecycle (SDL) tool integration
- support for official and unofficial builds
- feature flag system for controlled rollouts
- parameter validation with sensible defaults
- conditional logic for different build types (PR vs official)
- error handling with clear validation messages
- documenting of required vs optional parameters
