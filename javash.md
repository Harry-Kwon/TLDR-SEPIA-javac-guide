# TLDR how to compile and run java programs
(aka. Eclipse/Netbeans/IDEs are a pain, just use bash, [RTFM](https://docs.oracle.com/en/java/javase/13/docs/specs/man/javac.html#:~:text=Description,Java%20source%20files%20and%20classes.))

# Compiling your program
tldr: `javac -cp lib/Sepia.jar your/path/to/file/to/compile/filename.java`
Breaking it down:
- `-cp lib/Sepia.jar` <- this tells the compiler what libraries are referenced in your file
    - delimit multiple dependencies with `:`
    - ex. `-cp lib/Sepia.jar:lib/something_else.jar`
- you don't *have* to put your source files under src/ to compile them as long as you specify their location

# Running your program
- Note for SEPIA: before running SEPIA, make sure you set <Classname> to your compiled agent class in *_config.xml
tldr: `java -cp lib/Sepia.jar:src:otherclasspaths edu.cwru.sepia.Main2 data/MAZE_CONFIG_config.xml`

The class file of your agent must be in classpath (`-cp`) argument.

# Short example
Consider the following project structure:
```
data/
  maze_8x8_config.xml
  maze_8x8.xml
lib/
  Sepia.jar
src/
  edu/
    cwru/
      sepia/
        agent/
          AstarAgent.java
          EnemyBlockerAgent.class
```

To compile `AstarAgent.java`, run `javac -cp lib/Sepia.jar src/edu/cwru/sepia/agent/AstarAgent.java`.
This will create `AstarAgent.class`:

```
data/
  maze_8x8_config.xml
  maze_8x8.xml
lib/
  Sepia.jar
src/
  edu/
    cwru/
      sepia/
        agent/
          AstarAgent.java
          AstarAgent.class
          EnemyBlockerAgent.class
```

Before running SEPIA, edit your maze config `maze_8x8_config.xml` to direct it to your agent's class file:
`<Classname>edu.cwru.sepia.agent.AstarAgent</Classname>`.

And run SEPIA: `java -cp lib/Sepia.jar:src edu.cwru.sepia.Main2 data/maze_8x8_config.xml`

*One last note on classpath* notice that we had `src` in our classpath, and `edu.cwru.sepia.agent.AstarAgent` in our config file.
You can place your class files anywere as long as it is reachable from the config file. For example, if I had:
```
data/
lib/
src/
P2/
  AstarAgent.class
```
I could set `<Classname>AstarAgent</Classname>` in my config file and add `P2` to my classpath and run with:
`java -cp lib/Sepia.jar:src:P2 edu.cwru.sepia.Main2 data/maze_8x8_config.xml`

If you have any questions, don't be a dummy, [Read](https://docs.oracle.com/en/java/javase/13/docs/specs/man/javac.html#:~:text=Description,Java%20source%20files%20and%20classes.). [the](https://docs.oracle.com/javase/7/docs/technotes/tools/windows/classpath.html). [Docs](http://engr.case.edu/ray_soumya/sepia/html/setup.html#command-line-setup)
