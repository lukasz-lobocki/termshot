# termshot

Terminal screenshot tool, which takes the console output and renders an output image that resembles a user interface window. The idea is similar to what [carbon.now.sh](https://carbon.now.sh/), [instaco.de](http://instaco.de/), or [codekeep.io/screenshot](https://codekeep.io/screenshot) do. Instead of applying syntax highlight based on a programming language, `termshot` is using the ANSI escape codes of the program output. The result is clean screenshot (or recreation) of your terminal output.

Like `time`, `watch`, or `perf`, just place `termshot` before the command and you are set.

If you want, it has an option to `--edit` the program output before creating the screenshot. This way you can remove unwanted sensitive content.

You may specify the `--width` to control number of character colums in the output.

For example, `termshot --show-cmd -- lolcat -f <(figlet -f big foobar)` will create a screenshot which looks like this: ![example](.docs/images/example.png?raw=true "example screenshot")

## Notes

- Since both `termshot` and your command can have command line flags, it is recommended to use `--` to separate them.

  ```sh
  termshot --edit -- tool --apply --force
  ```

- If you want to run a command and pipe the output into another, you have to use quotes to make this clear on the command line.

  ```sh
  termshot --show-cmd -- "figlet foobar | lolcat"
  ```

- In order to work, `termshot` uses a pseudo terminal for the command to be executed. This means you can invoke a fully interactive shell and capture the entire output. The screenshot is created once you terminate the shell.

  ```sh
  termshot /bin/zsh
  ```

- _Please note:_ This project is work in progress. Although a lot of the ANSI sequences can be parsed, there are definitely commands in existence that create output that cannot be parsed correctly, yet. Also, commands that reset the cursor position are known to create issues.
