# Part mangement
This git contains a KiCad project environment that is suitable for managing the GitHub symbols and footprints for MySensors.

For working with (and referencing) the MySensors KiCad libraries you need to add an additional path configuration
to your project. The path must be named **MYSLOCAL** and it should point out the root of your cloned libraries.
As KiCad currently does not support symbols for it's github plugin you have to clone the symbols git explicitly.
So, if you have cloned your symbols to **~/gits/GitHub/mysensors-kicad/mysensors_symbols** you should create the path
**MYSLOCAL** and point it to **~/gits/GitHub/mysensors-kicad**. You only need to do this once and it is done in the main
KiCad app under **Preferences** - **Configure Paths**. Obviously this means you also need to manually *pull* any
updates in the symbol library in order to receive the updates to your computer.
On Windows, KiCad does not permit free-text entry to this location. Instead you have to edit your environment variables
and add a "User variable" named **MYSLOCAL** instead (with the appropriate value).  Now, define another path name 
**MYSGITHUB** with the path **https://github.com/mysensors-kicad** that we will use for footprints (see below)

The edit_parts.pro project is preconfigured to reference the symbol libraries as mentioned above but it will also
expect that you have globally defined paths to the footprint libraries. Having the paths globally applied free you
from the hassle of managing the MySensors libraries for each and every project you manage.

You set up the footprint repositories like this:
Add libraries using the Footprint Libraries Wizard and select GitHub repository but do **not** check the
*Save a local copy to:* box.

Edit your global fp-lib-table (on **Linux** systems this is located in *~/.config/kicad/fp-lib-table*, on **Windows**,
it is typically *C:\Users\<user>\AppData\Roaming\kicad\fp-lib-table*, and on Mac OS X it is in 
*~/Library/Preferences/kicad/fp-lib-table*) and locate the entries for the newly added libraries. 
They should look something like this:

```
  (lib (name mysensors_handsoldering)(type Github)(uri ${MYSGITHUB}/mysensors_handsoldering.pretty)(options allow_pretty_writing_to_this_dir=${MYSLOCAL}/mysensors_handsoldering.pretty)(descr "Various footprints adapted for handsoldering"))
  (lib (name mysensors_radios)(type Github)(uri ${MYSGITHUB}/mysensors_radios.pretty)(options allow_pretty_writing_to_this_dir=${MYSLOCAL}/mysensors_radios.pretty)(descr "RF modules supported by MySensors"))
  (lib (name mysensors_arduino)(type Github)(uri ${MYSGITHUB}/mysensors_arduino.pretty)(options "")(descr ""))
```
Add the following variable to the options string (note that ${HOME} is probably a Linux specific variable, you can change this to something that applies to your environment):
allow_pretty_writing_to_this_dir=${HOME}/<path-to-local-library-dir.pretty

**You also need to create the path you specify here.**

You may also if you like, add a description to the added libraries. When finished it should look something like this:
```
  (lib (name mysensors_arduino)(type Github)(uri ${MYSGITHUB}mysensors_arduino.pretty)(options "allow_pretty_writing_to_this_dir=${MYSLOCAL}/mysensors_arduino.pretty")(descr "Arduino footprints"))
  (lib (name mysensors_handsoldering)(type Github)(uri ${MYSGITHUB}/mysensors_handsoldering.pretty)(options "allow_pretty_writing_to_this_dir=${MYSLOCAL}/mysensors_handsoldering.pretty")(descr "Various footprints adapted for handsoldering"))
  (lib (name mysensors_radios)(type Github)(uri ${MYSGITHUB}/mysensors_radios.pretty)(options "allow_pretty_writing_to_this_dir=${MYSLOCAL}/mysensors_radios.pretty")(descr "RF modules supported by MySensors"))
  (lib (name mysensors_connectors)(type Github)(uri ${MYSGITHUB}/mysensors_connectors.pretty)(options "allow_pretty_writing_to_this_dir=${MYSLOCAL}/mysensors_connectors.pretty")(descr "Connector footprint modules used by MySensors"))
  (lib (name mysensors_leds)(type Github)(uri ${MYSGITHUB}/mysensors_leds.pretty)(options "allow_pretty_writing_to_this_dir=${MYSLOCAL}/mysensors_leds.pretty")(descr "LED footprint modules used by MySensors"))
  (lib (name mysensors_obscurities)(type Github)(uri ${MYSGITHUB}/mysensors_obscurities.pretty)(options "allow_pretty_writing_to_this_dir=${MYSLOCAL}/mysensors_obscurities.pretty")(descr "RF modules supported by MySensors"))
```

Now, any changes you make to the footprints in these libraries will be saved locally to the path you have specified.
If you are the library maintainer, you can clone the repository directly to this path in order to simplify repository management.


