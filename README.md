# IEEE754-homeassistant

Home Assistant Jinja macro for converting [IEEE 754](https://en.wikipedia.org/wiki/IEEE_754) hex strings to floating-point decimal that will handle
[half](https://en.wikipedia.org/wiki/Half-precision_floating-point_format),
[single](https://en.wikipedia.org/wiki/Single-precision_floating-point_format),
and [double](https://en.wikipedia.org/wiki/Double-precision_floating-point_format) precision formats.

This is intended for installation as a [reusable template](https://www.home-assistant.io/docs/configuration/templating/#reusing-templates):

* Create the folder `/config/custom_templates`;
* Download or copy/paste [this `ieee754.jinja` file](https://raw.githubusercontent.com/Troon/IEEE754-homeassistant/main/ieee754.jinja) into that folder;
* Reload by either restarting HA or calling the `homeassistant.reload_custom_templates` service ([link to do this on your system](https://my.home-assistant.io/redirect/_change/?redirect=developer_call_service%2F%3Fservice%3Dhomeassistant.reload_custom_templates)).

Then you can use it like this:

```
{% from 'ieee754.jinja' import ieee754_float %}
{{ ieee754_float("4248") }}
{{ ieee754_float("fl_40490fdb") }}
{{ ieee754_float("4009 21FB 5444 2D18") }}
```

It handles spacing in the hex and an optional `fl_` prefix as used by Senec systems.
The infinity and `nan` special cases both return None / `null` as Jinja has no sentinel
value for infinity.

As with all such macros, the return value is a string, and will need casting before
used in calculations. For example:

```
{% from 'ieee754.jinja' import ieee754_float %}
{{ ieee754_float("4037 0000 0000 0000")|int + 19 }}
```

Also contains first-draft macros `float_ieee754_single(float)` and `float_ieee754_double(float)` to convert in the other direction:
```
{% from 'ieee754.jinja' import float_ieee754_single %}
{{ float_ieee754_single(-6.2598534e+18) }}
```
