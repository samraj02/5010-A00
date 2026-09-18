# LLM Code Evaluation Report — Assignment 0: Setup

## Student Information

- **Name**: Samraj Aneja
- **Date**: 2026-09-18
- **LLM Used**: Claude

## Prompt Used

The prompt from `LLM-Evaluation-prompt.md` with my name filled in and then i asked it to look at the files greeting.java and run it to see the output.

## What the LLM said

Good news up front: everything here is correct and your setup is working. Taking your four
questions in order.

**1. Does `message()` return a greeting with your name in it?**

Yes. Line 15 of `Greeting.java` reads `private static final String STUDENT_NAME = "Samraj Aneja";`
— the `"YOUR NAME HERE"` placeholder is gone. The exact string `message()` returns is:

```
Hello, Java! — Samraj Aneja
```

Two details worth noticing: the separator is an em dash (`—`), not a hyphen, and there is a space on
each side of it. Your `./gradlew run` output prints that same string character for character, which
tells you the class that actually compiled and ran is the one you edited — not a stale build.

**2. Will the two JUnit tests pass?**

Both of them, yes.

- **`messageNamesTheStudent` — PASS.** It asserts two things. `"Hello, Java! — Samraj Aneja"` has
  visible characters, so `assertFalse(message.isBlank())` holds. And the string does not contain the
  substring `"YOUR NAME HERE"` anywhere, so `assertFalse(message.contains("YOUR NAME HERE"))` holds
  too. This is the test that fails on a fresh clone; your edit is exactly what turns it green.
- **`messageHasGreetingPrefix` — still PASS.** It asserts
  `message().startsWith("Hello, Java!")`. You only changed the constant on the end of the
  concatenation; the literal prefix `"Hello, Java! — "` is untouched, so this test is unaffected by
  your edit. It was green before and it is green now.

Your run confirms both: 2 tests, 0 failures, 0 errors, 0 skipped.

**3. `STUDENT_NAME` and `message()` in your own words**

`STUDENT_NAME` is a constant — `private static final` means one fixed value, owned by the class
itself rather than by any object, and not visible outside the class. `message()` is a `static`
method that builds the greeting by joining the fixed text `"Hello, Java! — "` to that constant and
returning the result, which `Main` then prints.

If a grader pushes on it during the walk, the useful extra sentence is: the class is `final` with a
private constructor, which makes it a _utility class_ — you never construct a `Greeting`, you call
`Greeting.message()` on the class itself.

**4. Was the tool output a clean run?**

Yes, clean on all three counts — and running `clean` first was a good instinct, because it rules out
any chance you were reading cached results from an earlier build.

- **Tests green.** `:test` ran and the build reported `BUILD SUCCESSFUL`. Gradle fails the build
  when a test fails, so a `:test` task that completes without a failure report _is_ the green
  signal. The results XML backs it up: 2 run, 0 failed.
- **Coverage report generated.** `:jacocoTestReport` executed and wrote
  `build/reports/jacoco/test/html/index.html` (plus the XML alongside it).
- **Checkstyle report generated.** `:checkstyleMain` executed and wrote
  `build/reports/checkstyle/main.html` and `main.xml`. I checked the XML: **zero** `<error>`
  entries, so there are genuinely no style violations in `src/main`.
- **JDK is right.** Your toolchain reports JVM **21.0.12.1** on Gradle 8.14. The course requires
  JDK 21, so there is nothing to re-check — no wrapper problem, no version mismatch.

Nothing is wrong, but three things are worth filing away:

1. **A green `checkstyleMain` is not by itself proof of a clean style report.** Your `build.gradle`
   sets `ignoreFailures = true` in the `checkstyle` block, so the task would print
   `BUILD SUCCESSFUL` even with violations present. Yours really is clean — I read the report to
   confirm rather than inferring it from the build status — but from A1 on, open
   `build/reports/checkstyle/main.html` and look.
2. **You repointed checkstyle at `config/checkstyle/northeastern_checks.xml`** instead of the
   template's `config/checkstyle/checkstyle.xml`. That is the correct ruleset for this course, but
   it is a deliberate change to a shipped file — say so in the code walk so nobody reads it as an
   accident.
3. **The instructions have a stale path.** Both `LLM-Evaluation-prompt.md` and `how-to-submit.md`
   refer to `src/main/java/edu/northeastern/sketchpad/Greeting.java`, but the package in this
   template is `edu.northeastern.setup`. Your file is in the right place; the docs are what is out
   of date. Copy from the `setup` path when you fill in `submission/`.

One cosmetic note, offered rather than applied since you asked me not to rewrite anything: in the
Javadoc block above `message()` (lines 21–25), the continuation asterisks sit one column left of the
opening `/**`, so the block does not line up on screen. Checkstyle does not flag it. It is a
two-space fix if you want the file to look tidy while you are sharing your screen.

## Your checklist

- **`./gradlew run` prints the greeting with my name?**: Yes
- **`./gradlew test` is green?**: Yes
- **Coverage + checkstyle reports generated?**: Yes
- **I can explain what `Greeting.message()` returns and why the test passes?**: Yes, becuase I filled it my name ans the assertion we were checking against the template string is returning false like we wanted.

## Reflection

The only issue i had was with the checklist, i think the one the project ships with and then one that northeastern gave us in the setup are different and for that reason i was getting an error in the function definition in greetings, which i amended.
