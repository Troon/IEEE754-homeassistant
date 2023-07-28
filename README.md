# IEEE754-homeassistant

Home Assistant Jinja macro for converting [IEEE 754](https://en.wikipedia.org/wiki/IEEE_754) hex strings to floating-point decimal that will handle
[half](https://en.wikipedia.org/wiki/Half-precision_floating-point_format),
[single](https://en.wikipedia.org/wiki/Single-precision_floating-point_format),
and [double](https://en.wikipedia.org/wiki/Double-precision_floating-point_format) precision formats.

This is intended for installation as a [reusable template](https://www.home-assistant.io/docs/configuration/templating/#reusing-templates):

* Create the folder `/config/custom_templates`
* Download or copy/paste [this `ieee754.jinja` file](https://raw.githubusercontent.com/Troon/IEEE754-homeassistant/main/ieee754.jinja) into that folder.
* Reload by either restarting HA or calling the `homeassistant.reload_custom_templates` service ([link to do this on your system](https://my.home-assistant.io/redirect/_change/?redirect=developer_call_service%2F%3Fservice%3Dhomeassistant.reload_custom_templates)).

Then you can use it like this:

```
{% from 'ieee754.jinja' import ieee754 %}
{{ ieee754("7bff") }}
{{ ieee754("fl_43F54001") }}
{{ ieee754("4037 0000 0000 0000") }}
```

It handles spacing in the hex and an optional `fl_` prefix as used by Senec systems.
Note that it does not currently deal with invalid input strings, nor the 
infinity or `nan` special cases.
