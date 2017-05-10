# Grbl support for OctoPrint

This plugin lets you use Grbl based CNC machines with OctoPrint.

**NOTE:** You still need to set a few more settings after installing
this plugin to make it work. See below.

## Installation

```bash
pip install octoprint-grbl-plugin
```

## Required Configuration

- _Serial Connection_ > _Advanced options_ > _"Hello" command_ = **M5**
- _Features_ > _Send a checksum with the command_ > **Never**


## Additional controls

If you would like to show some additional info on the "Control" tab,
add the following to your `config.yaml` file:

```yaml
controls:
- name: State
  type: section
  layout: vertical
  children:
  - name: Realtime State
    # <Idle,MPos:0.000,0.000,0.000,WPos:0.000,0.000,0.000,RX:3,0/0>
    regex: '<([^,]+),MPos:([+\-\d.]+,[+\-\d.]+,[+\-\d.]+),WPos:([+\-\d.]+,[+\-\d.]+,[+\-\d.]+)'
    template: 'State: {0}  Machine Position: {1}  Work Position: {2}'
    type: feedback
  - name: GCode state
    # [G0 G54 G17 G21 G90 G94 M0 M5 M9 T0 F300. S700.]
    regex: 'F([\d.]+) S([\d.]+)'
    template: 'Speed: {0}  Power: {1}'
    type: feedback
  - command: '?$G'
    name: Refresh
```