name: Task
about: Track a new task, doc, or fix
title: ""
labels: []
assignees: []

body:
  - type: textarea
    id: what
    attributes:
      label: What
      description: What is being added/changed?
      placeholder: Short description of the task
    validations:
      required: true

  - type: textarea
    id: why
    attributes:
      label: Why
      description: Why is this needed? What problem does it solve?
      placeholder: Reason or motivation
    validations:
      required: true

  - type: textarea
    id: notes
    attributes:
      label: Notes
      description: Extra context, caveats, or references
      placeholder: n/a
    validations:
      required: false

