# AB Veterinary Job

A configurable veterinary job resource for RedM built for VORP Core.

AB Veterinary Job is designed to provide structured veterinary roleplay rather than a simple interaction-and-payment system. Players are required to properly examine, diagnose, treat, and reassess animals while responding to veterinary calls throughout configured regions.

The resource is designed with roleplay, server performance, configurability, and anti-farming protections in mind.

## Author

AllieBabyDev

## Framework

VORP Core

## Resource

`AB_veterinary`

## Overview

The veterinary system provides players with an interactive job centered around responding to injured or sick animals throughout the world.

Veterinarians clock into duty, receive randomized veterinary calls, travel to the reported location, examine the animal, collect samples when required, determine treatment, perform the appropriate care, and reassess the animal before completing the call.

The system is intended to create actual veterinary roleplay rather than allowing players to repeatedly interact with animals for instant payouts.

## Current Features

### Veterinary Duty System

Veterinarians can clock in and out using:

```text
/vetduty
```

The current veterinary workplace is based around the Valentine stable.

Only players with the configured veterinary job can use the veterinary duty system.

The default supported job grade begins at grade `0`.

### Workplace Anti-Farming Protection

Veterinarians are expected to remain within the configured workplace area while working.

If an on-duty veterinarian remains outside the allowed workplace radius for an extended period, the system automatically removes them from duty.

The current automatic clock-out timer is approximately five minutes outside the configured area.

This prevents players from remaining on duty indefinitely simply to collect job benefits or payments.

### Random Veterinary Dispatches

Veterinary calls are generated automatically while eligible veterinarians are on duty.

Calls are intentionally randomized rather than being sent continuously.

The system is designed around a configurable delay between calls so veterinarians are not immediately overwhelmed with multiple incidents.

Additional calls can also be limited based on the number of already-active veterinary calls.

This allows servers to control how busy the veterinary workload becomes.

### Regional Animal Calls

Veterinary incidents can be configured across multiple locations and regions.

Current example areas include:

- Heartlands pasture
- Heartlands meadow
- Emerald countryside
- Big Valley
- Rhodes countryside

Each location can have its own supported animal types.

Current supported examples include:

- Horses
- Cattle
- Sheep
- Deer
- Goats

Additional regions and animal types can be added through the configuration.

## Veterinary Treatment Flow

Veterinary calls follow a structured treatment process.

### 1. Examination

The veterinarian approaches the animal and performs an initial physical examination.

The examination system uses a crouched inspection animation to better represent physically examining the animal.

Current inspection animation:

```text
amb_work@world_human_crouch_inspect@female_a@idle_a
```

Animation:

```text
idle_a
```

The veterinarian must remain within the configured interaction distance to perform the examination.

### 2. Blood Sample

Certain veterinary cases require a blood sample before treatment can continue.

The blood draw uses an actual Red Dead Redemption 2 animation and syringe prop.

Animation dictionary:

```text
mech_skin@sample@base
```

Animation:

```text
sample_mid
```

Syringe prop:

```text
p_cs_syringe02x
```

The system handles loading and removing the prop when the interaction is completed.

### 3. Sample Testing

After collecting a sample, the veterinarian performs a testing interaction.

The testing process uses a journal-style writing animation to represent recording or reviewing veterinary results.

### 4. Treatment

Once the condition has been identified, the veterinarian performs the appropriate treatment based on the veterinary case.

Treatment logic can be configured or expanded with additional case types.

The system is structured so players cannot simply skip directly to the completion stage.

### 5. Reassessment

After treatment, the veterinarian must reassess the animal.

The reassessment process uses the veterinary journal animation to represent recording the animal's response to treatment and completing the final evaluation.

The veterinary call is only completed after the required treatment sequence has been performed.

## Interaction Distance Protection

Veterinary interactions verify the player's distance from the animal.

If the veterinarian moves too far away, the interaction will not continue and the player will be instructed to move closer.

This prevents veterinary actions from being performed from unrealistic distances.

## Veterinary Payments

The resource supports configurable veterinary payouts.

Payments can be configured based on animal species or veterinary case.

The resource can support:

- On-duty hourly payment
- Completed veterinary call payments
- Species-based payouts

The veterinary payroll system is handled independently from external workplace payroll resources.

This allows AB Veterinary Job to function without requiring server owners to install a separate payroll script.

## Animal Scaling

Spawned veterinary animals can use configurable scaling.

The current veterinary animal scale has been adjusted to approximately:

```lua
0.86
```

This can be modified depending on the animal models being used by the server.

## Configurable Locations

Veterinary call locations are controlled through the configuration file.

Example structure:

```lua
Config.Locations = {
    {
        name = 'Heartlands pasture',
        x = -360.0,
        y = 710.0,
        z = 116.0,
        heading = 90.0,
        animals = {
            'horse',
            'cow',
            'sheep'
        }
    }
}
```

Server owners can add additional veterinary regions without modifying the main client logic.

## Call Management

The call system includes protections intended to prevent excessive veterinary spawns.

Configuration can control:

- Minimum time between calls
- Maximum time between calls
- Number of active veterinary calls
- Whether another call should be created
- Veterinary call cooldowns
- Supported animals per location

The system can also be configured so additional calls are only created when the number of active calls falls below a specified threshold.

## User Interface

The resource includes a custom NUI interface for veterinary duty and job information.

The interface has been redesigned to provide a cleaner and more organized veterinary panel rather than relying entirely on basic notifications or chat commands.

The UI can be further customized through the included HTML, CSS, and JavaScript files.

## Debugging

The resource includes configurable debugging functionality.

Debug mode can be enabled through the configuration file while developing or testing the resource.

Example:

```lua
Config.Debug = true
```

Debug tools are intended to help developers identify problems with:

- Veterinary call generation
- Animal spawning
- Interaction distances
- Duty state
- Animations
- Props
- Call progression

A veterinary animation testing command has also been used during development:

```text
/vetanimtest
```

This allows animation behavior to be tested without requiring a complete veterinary call.

Debug mode should normally be disabled on a production server unless troubleshooting is required.

## Configuration

Most major systems are intended to be configurable without directly editing the primary client or server files.

Configuration options may include:

- Veterinary job name
- Required job grade
- Workplace coordinates
- Workplace radius
- Automatic duty removal timer
- Veterinary call locations
- Supported animals
- Dispatch intervals
- Maximum active calls
- Interaction distance
- Animal scaling
- Payments
- Debug mode

## Resource Structure

The resource currently contains files similar to:

```text
AB_veterinary/
│
├── fxmanifest.lua
├── config.lua
├── client.lua
├── server.lua
├── README.md
│
└── html/
    ├── index.html
    ├── style.css
    └── app.js
```

File structure may vary depending on the installed version.

## Installation

Place the resource inside your RedM resources directory.

Example:

```text
resources/[AB]/AB_veterinary
```

Add the resource to your server configuration:

```text
ensure AB_veterinary
```

Ensure VORP Core and any required dependencies are started before AB Veterinary Job.

Restart the server or start the resource manually after installation.

## Requirements

The resource is designed for:

```text
RedM
VORP Core
```

Additional requirements should be listed here if future versions introduce external dependencies.

## Development Philosophy

AB Veterinary Job is designed around meaningful veterinary roleplay.

The goal is not to provide players with a button that instantly treats an animal and generates money.

The resource instead encourages players to work through a veterinary process:

```text
Examine
→ Collect Sample
→ Test
→ Diagnose
→ Treat
→ Reassess
→ Complete Call
```

Future development will continue to focus on expanding the variety of veterinary cases, improving immersion, and providing server owners with flexible configuration options.

## Planned Development

Potential future additions may include:

- Additional veterinary conditions
- Expanded treatment types
- More animal species
- Additional veterinary regions
- Improved case randomization
- Veterinary experience or progression
- Advanced diagnostic results
- Medical supply requirements
- Veterinary records
- Additional animations
- Improved dispatch management
- Expanded user interface
- Administrative veterinary controls

Planned features are subject to change during development.

## Support

When reporting an issue, provide as much information as possible.

Useful information includes:

```text
Resource version
VORP version
Error message
Client or server console output
Steps required to reproduce the issue
Whether debug mode is enabled
```

Issues that cannot be reproduced may require additional debugging information.

## Versioning

AB Veterinary Job uses versioned releases.

Example:

```text
v1.0.0
v1.1.0
v1.2.0
```

Major updates, fixes, and changes should be documented through the project's changelog or GitHub release notes.

## License and Distribution

Do not redistribute, resell, or reupload modified versions of this resource without permission from the original author.

Author:

```text
AllieBabyDev
```
