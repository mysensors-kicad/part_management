# Part mangement
This git contains a KiCad project environment that is suitable for managing the GitHub symbols and footprints for MySensors.

For working with (and referencing) the MySensors KiCad libraries you need to add an additional path configuration
to your project. The path must be named **MYSLOCAL** and it should point out the root of your cloned libraries.
As KiCad currently does not support symbols for it's github plugin you have to clone the symbols git explicitly.
So, if you have cloned your symbols to **~/gits/GitHub/mysensors-kicad/mysensors_symbols** you should create the path
**MYSLOCAL** and point it to **~/gits/GitHub/mysensors-kicad**. You only need to do this once and it is done in the main
KiCad app under **Preferences** - **Configure Paths**.

The edit_parts.pro project is preconfigured to reference the symbol libraries as mentioned above but it will also
have to be updated when new symbol libraries are created as these are listed in the project file itself.
You can add new libraries using the schematic library editor and via **Preferences** and **Component libraries**.

Project specific footprint libraries have been added for this project in order to distinguish footprints you want to
edit from footprints managed by the KiCad github plugin (if you have set up your environment to reference those).
These libraries have received the **_for_editing** suffix in order to make this distinction and they are expected to
reside **next to** this project. That is, you are expected to clone all the github projects next to each other.
Unfortunately, the footprint library manager does not adhere to the user-created **MYSLOCAL** variable
so we have to reference the footprint libraries relative to the project instead.

If you want to add new footprint libraries to this project for editing (and you shoud if you have added new footprint
libraries), edit the **fp-lib-table** file. Also note that you will need to add the GitHub repository using the KiCad Footprint
libraries wizard if you also want to use those.

For your own projects, it is highly recommended that you only reference the GitHub repositories as those paths can be
made more environment independent. These can be added to your global foot print search paths (selectable in the
footprint libraries wizard). Note that you still need to use the **MYSLOCAL** variable to reference the symbols if you
want to simplify other MySensor "users" to use/view your design.


