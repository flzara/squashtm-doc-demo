# CSS Guidelines

## Avoid inlined styles

For performance (and DRY) reasons, avoid inlined styles. There already are some classes you can use. Otherwise, create specific ones.

## CSS Minification

Stylesheets are processed using the wro4j maven plugin. Wro4j generates a squash.core.css and a couple of squash.<color>.css, which contain the concatenated, minified css classes.

When creating a page template, you simply need to import both the squash.core.css and the appropriate squash.<color>.css stylesheets.

If you need to add a new color pattern to Squash TM, you should define a "group" in src/main/webapp/WEB-INF/wro.xml which references the new color of the pattern files. Simply copy/paste an existing group and change the names. You should also make the wro4j maven plug-in process this new group by adding it to tm.web's pom.xml (see below).

    <plugin>    <groupId>ro.isdc.wro4j</groupId>    <artifactId>wro4j-maven-plugin</artifactId>    <version>${wro4j.version}</version>    <executions>      <execution>        <id>wro</id>        ...        <configuration>          <targetGroups>squash.core,squash.blue,...,squash.newgroup</targetGroups>          ...        </configuration>        ...

Note: The <targetGroup> element needs to be written on a single line with no spaces around the commas, otherwise it will not be parsed correctly.