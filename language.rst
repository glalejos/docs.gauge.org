Language Features
=================

.. note::

  Some behaviour of the language runners can be configured. See :ref:`Configuring Language Runner <language_config>` for details.

.. _language-steps:

Step implementations
--------------------

:ref:`longstart-steps` have a language specific implementation that gets executed on the spec execution.

Simple step
^^^^^^^^^^^

**Step name**

.. code-block:: gauge

  * Say "hello" to "gauge"

**Implementation**

.. container:: code-snippet

  .. tabs::

    .. group-tab:: C#

      .. code-block:: java

          // The Method can be written in **any C# class** as long as it is part of the project.
          public class StepImplementation {

            [Step("Say <greeting> to <product name>")]
            public void HelloWorld(string greeting, string name) {
                // Step implementation
            }
          }

    .. group-tab:: Java

      .. code-block:: java

          // This Method can be written in any java class as long as it is in classpath.

          public class StepImplementation {

            @Step("Say <greeting> to <product name>")
            public void helloWorld(String greeting, String name) {
                // Step implementation
            }

          }

    .. group-tab:: JavaScript

      .. code-block:: javascript

          step("Say <greeting> to <name>", async function(greeting, name) {
            throw 'Unimplemented Step';
          });

    .. group-tab:: Python

      .. code-block:: python

          @step("Say <greeting> to <product name>")
          def create_following_characters(greeting, name):
              assert False, "Add implementation code"

    .. group-tab:: Ruby

      .. code-block:: ruby

          step 'Say <greeting> to <product name>' do |greeting, name|
          # Code for the step
          end

Step with table
^^^^^^^^^^^^^^^

**Step**

.. code-block:: gauge

  * Create following "hobbit" characters
    |id |name   |
    |---|-------|
    |123|frodo  |
    |456|bilbo  |
    |789|samwise|

**Implementation**

.. container:: code-snippet

  .. tabs::

    .. group-tab:: C#

      .. code-block:: java

        // Here Table is a custom data structure defined by gauge.
        // This is available by adding a reference to the Gauge.CSharp.Lib.
        // Refer : http://nuget.org/packages/Gauge.CSharp.Lib/

        public class Users {

          [Step("Create following <role> users <table>")]
          public void HelloWorld(string role, Table table) {
              // Step implementation
          }

        }

    .. group-tab:: Java

      .. code-block:: java

        // Table is a custom data structure defined by gauge.
        public class Users {

          @Step("Create following <race> characters <table>")
          public void createCharacters(String type, Table table) {
              // Step implementation
          }

        }

    .. group-tab:: JavaScript

      .. code-block:: javascript

        step("Create following <arg0> characters <arg1>", async function(arg0, arg1) {
          throw 'Unimplemented Step';
        });

    .. group-tab:: Python

      .. code-block:: python

        # Here Table is a custom data structure defined by gauge.

        @step("Create following <hobbit> characters <table>")
        def create_following_characters(hobbit, table):
            assert False, "Add implementation code"

    .. group-tab:: Ruby

      .. code-block:: ruby
        :caption: Ruby

        # Here table is a custom data structure defined by gauge-ruby.

        step 'Create following <race> characters <table>' do |role, table|
          puts table.rows
          puts table.columns
        end




.. _execution_hooks:

Execution hooks
---------------

Test execution hooks can be used to run arbitrary test code as different
levels during the test suite execution.

**Implementation**

.. container:: code-snippet

  .. tabs::

    .. group-tab:: C#

      .. code-block:: java

        public class ExecutionHooks
        {

          [BeforeSuite]
          public void BeforeSuite() {
            // Code for before suite
          }

          [AfterSuite]
          public void AfterSuite() {
            // Code for after suite
          }

          [BeforeSpec]
          public void BeforeSpec() {
            // Code for before spec
          }

          [AfterSpec]
          public void AfterSpec() {
            // Code for after spec
          }

          [BeforeScenario]
          public void BeforeScenario() {
            // Code for before scenario
          }

          [AfterScenario]
          public void AfterScenario() {
            // Code for after scenario
          }

          [BeforeStep]
          public void BeforeStep() {
            // Code for before step
          }

          [AfterStep]
          public void AfterStep() {
            // Code for after step
          }

        }

    .. group-tab:: Java

      .. code-block:: java

        public class ExecutionHooks {

          @BeforeSuite public void BeforeSuite() {
            // Code for before suite
          }

          @AfterSuite
          public void AfterSuite() {
            // Code for after suite
          }

          @BeforeSpec
          public void BeforeSpec() {
            // Code for before spec
          }

          @AfterSpec
          public void AfterSpec() {
            // Code for after spec
          }

          @BeforeScenario
          public void BeforeScenario() {
            // Code for before scenario
          }

          @AfterScenario
          public void AfterScenario() {
            // Code for after scenario
          }

          @BeforeStep
          public void BeforeStep() {
            // Code for before step
          }

          @AfterStep
          public void AfterStep() {
            // Code for after step
          }

        }

    .. group-tab:: JavaScript

      .. code-block:: javascript

        hooks.beforeSuite(fn, [opts]) {
          // Code for before suite
        }

        hooks.beforeSpec(fn, [opts]) {
          // Code for before spec
        }

        hooks.beforeScenario(fn, [opts]) {
          // Code for before scenario
        }

        hooks.beforeStep(fn, [opts]) {
          // Code for before step
        }

        hooks.afterSuite(fn, [opts]) {
          // Code for after suite
        }

        hooks.afterSpec(fn, [opts]) {
          // Code for after spec
        }

        hooks.afterScenario(fn, [opts]) {
          // Code for after scenario
        }

        hooks.afterStep(fn, [opts]) {
          // Code for after step
        }

    .. group-tab:: Python

      .. code-block:: python

        from getgauge.python import before_step, after_step, before_scenario, after_scenario, before_spec, after_spec, before_suite, after_suite

        @before_step
        def before_step_hook():
            print("before step hook")

        @after_step
        def after_step_hook():
            print("after step hook")

        @before_scenario
        def before_scenario_hook():
            print("before scenario hook")

        @after_scenario
        def after_scenario_hook():
            print("after scenario hook")

        @before_spec
        def before_spec_hook():
            print("before spec hook")

        @after_spec
        def after_spec_hook():
            print("after spec hook")

        @before_suite
        def before_suite_hook():
            print("before suite hook")

        @after_suite
        def after_spec_hook():
            print("after suite hook")

    .. group-tab:: Ruby

      .. code-block:: ruby

        before_suite do
          # Code for before suite
        end

        after_suite do
          # Code for after suite
        end

        before_spec do
          # Code for before spec
        end

        after_spec do
          # Code for after spec
        end

        before_scenario do
          # Code for before scenario
        end

        after_scenario do
          # Code for after scenario
        end

        before_step do
          # Code for before step
        end

        after_step do
          # Code for after step
        end


By default, Gauge clears the state after each scenario so that new
objects are created for next scenario execution. You can :ref:`configure <default_properties>`
to change the level at which Gauge clears cache.

Current Execution Context in the Hook
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

-  To get additional information about the **current specification,
   scenario and step** executing, an additional **ExecutionContext**
   parameter can be added to the :ref:`hooks <execution_hooks>` method.

.. container:: code-snippet
    .. tabs::

        .. group-tab:: C#

            .. code-block:: java

                This feature is not yet
                supported in Gauge-CSharp. Please refer to
                https://github.com/getgauge/gauge-csharp/issues/53 for updates.

        .. group-tab:: Java

            .. code-block:: java

                @BeforeScenario
                public void loginUser(ExecutionContext context) {
                String scenarioName = context.getCurrentScenario().getName();
                // Code for before scenario
                }

                @AfterSpec
                public void performAfterSpec(ExecutionContext context) {
                Specification currentSpecification = context.getCurrentSpecification();
                // Code for after step
                }

        .. group-tab:: JavaScript

            .. code-block:: javascript

                hooks.beforeScenario(fn, [opts]) { ... }
                hooks.afterSpec(fn, [opts]) { ... }

        .. group-tab:: Python

            .. code-block:: python

                from getgauge.python import before_step, after_scenario

                @before_scenario
                def before_scenario_hook():
                    print("before scenario hook")

                @after_spec
                def after_spec_hook():
                    print("after spec hook")

        .. group-tab:: Ruby

            .. code-block:: ruby

                before_spec do |execution_info|
                    puts execution_info.inspect
                end

                after_spec do |execution_info|
                    puts execution_info.inspect
                end


.. _filtering_hooks_with_tags:

Filtering Hooks execution based on tags
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

-  You can specify tags for which the execution :ref:`hooks <execution_hooks>` can run. This
   will ensure that the hook runs only on scenarios and specifications
   that have the required tags.
.. container:: code-snippet

    .. tabs::

        .. group-tab:: C#

            .. code-block:: java

                // A before spec hook that runs when tag1 and tag2
                // is present in the current scenario and spec.
                [BeforeSpec("tag1, tag2")]
                public void LoginUser() {
                    // Code for before scenario
                }

                // A after step hook runs when tag1 or tag2
                // is present in the current scenario and spec.
                // Default tagAggregation value is Operator.AND.
                [AfterStep("tag1", "tag2")]
                [TagAggregationBehaviour(TagAggregation.Or)]
                public void PerformAfterStep() {
                    // Code for after step
                }
        .. group-tab:: Java

            .. code-block:: java

                // A before spec hook that runs when tag1 and tag2
                // is present in the current scenario and spec.
                @BeforeSpec(tags = {"tag1, tag2"})
                public void loginUser() {
                    // Code forbefore scenario
                }

                // A after step hook runs when tag1 or tag2
                // is present in the currentscenario and spec.
                // Default tagAggregation value is Operator.AND.
                @AfterStep(tags = {"tag1", "tag2"}, tagAggregation = Operator.OR)
                public void performAfterStep() {
                    // Code for after step
                }

        .. group-tab:: JavaScript

            .. code-block:: javascript

                // A before spec hook that runs when tag1 and tag2
                // is present in the current scenario and spec.
                hooks.beforeSpec(function () {
                    //implementation
                }, { tags: [ "tag1","tag2" ]});

                // A after step hook runs when tag1 or tag2
                // is present in the currentscenario and spec.
                // Default tagAggregation value is Operator.AND.
                hooks.afterStep(function () {
                    //implementation
                }, { tags: [ "tag1","tag2" ]});

        .. group-tab:: Python

            .. code-block:: python

                // A before spec hook that runs when tag1 and tag2
                // is present in the current scenario and spec.
                @before_spec("<tag1> and <tag2>")
                def before_spec_hook():
                    print("before spec hook with tag")

                // A after step hook runs when tag1 or tag2
                // is present in the currentscenario and spec.
                // Default tagAggregation value is Operator.AND.
                @after_step("<tag1> and <tag2>")
                def after_step_hook():
                    print("after step hook with tag")
        .. group-tab:: Ruby

            .. code-block:: ruby

                # A before spec hook that runs when
                # tag1 and tag2 is present in the current scenario and spec.
                before_spec({tags: ['tag2', 'tag1']}) do
                    # Code for before scenario
                end

                # A after step hook runs when tag1 or tag2 is present in the current scenario and spec.
                # Default tagAggregation value is Operator.AND.

                after_spec({tags: ['tag2', 'tag1'], operator: 'OR'}) do
                    # Code for after step
                end

.. note:: Tags cannot be specified on @BeforeSuite and @AfterSuite hooks


Data Store
----------

Data (Objects) can be shared in steps defined in different classes at
runtime using DataStores exposed by Gauge.

There are 3 different types of DataStores based on the lifecycle of when
it gets cleared.

ScenarioStore
^^^^^^^^^^^^^

This data store keeps values added to it in the lifecycle of the
scenario execution. Values are cleared after every scenario executes

.. container:: code-snippet

  .. tabs::

    .. group-tab:: C#

      .. code-block:: java

        using Gauge.CSharp.Lib;

        // Adding value
        var scenarioStore = DataStoreFactory.ScenarioDataStore;
        scenarioStore.Add("element-id", "455678");

        // Fetching Value
        var elementId = (string) scenarioStore.Get("element-id");

        // avoid type cast by using generic Get
        var anotherElementId = scenarioStore.Get("element-id");

    .. group-tab:: Java

      .. code-block:: java

        import com.thoughtworks.gauge.datastore.*;

        // Adding value
        DataStore scenarioStore = DataStoreFactory.getScenarioDataStore();
        scenarioStore.put("element-id", "455678");

        // Fetching Value
        String elementId = (String) scenarioStore.get("element-id");

    .. group-tab:: JavaScript

      .. code-block:: javascript

        // Adding value
        gauge.dataStore.scenarioStore.put(key, value);

        // Fetching Value
        gauge.dataStore.scenarioStore.get(key);

    .. group-tab:: Python

      .. code-block:: python
        :caption: python

        from getgauge.python import DataStoreFactory
        // Adding value
        DataStoreFactory.scenario_data_store().put(key, value)

        // Fetching Value
        DataStoreFactory.scenario_data_store().get(key)

    .. group-tab:: Ruby

      .. code-block:: ruby

        // Adding value
        scenario_store = DataStoreFactory.scenario_datastore;
        scenario_store.put("element-id", "455678");


        // Fetching Value
        element_id = scenario_store.get("element-id");


SpecStore
^^^^^^^^^

This data store keeps values added to it during the lifecycle of the
specification execution. Values are cleared after every specification
executes

.. container:: code-snippet

  .. tabs::

    .. group-tab:: C#

      .. code-block:: java

        using Gauge.CSharp.Lib;

        // Adding value
        var specStore = DataStoreFactory.SpecDataStore;
        specStore.Add("element-id", "455678");

        // Fetching Value
        var elementId = (string) specStore.Get("element-id");

        // avoid type cast by using generic Get
        var anotherElementId = specStore.Get("element-id");

    .. group-tab:: Java

      .. code-block:: java

        // Import Package import
        com.thoughtworks.gauge.datastore.*;

        // Adding value DataStore specStore =
        DataStoreFactory.getSpecDataStore();
        specStore.put("key", "455678");

        // Fetching value DataStore specStore =
        String elementId = (String) specStore.get("key");

    .. group-tab:: JavaScript

      .. code-block:: javascript

        // Adding value DataStore specStore =
        gauge.dataStore.specStore.put(key, value);
        // Fetching value DataStore specStore =
        gauge.dataStore.specStore.get(key);

    .. group-tab:: Python

      .. code-block:: python

        // Import Package import
        from getgauge.python import DataStoreFactory
        // Adding value DataStore specStore =
        DataStoreFactory.spec_data_store().put(key, value)

        // Fetching value DataStore specStore =
        DataStoreFactory.spec_data_store().get(key)

    .. group-tab:: Ruby

      .. code-block:: ruby

        // Adding value
        spec_store = DataStoreFactory.spec_datastore;
        spec_store.put("element-id", "455678");

        // Fetching Value
        element_id = spec_store.get("element-id");

SuiteStore
^^^^^^^^^^

This data store keeps values added to it during the lifecycle of entire
suite execution. Values are cleared after entire suite execution.

.. warning::
   ``SuiteStore`` is not advised to be used when executing specs in parallel.
   The values are not retained between parallel streams of execution.

.. container:: code-snippet

  .. tabs::

    .. group-tab:: C#

      .. code-block:: java

        using Gauge.CSharp.Lib;

        // Adding value var suiteStore = DataStoreFactory.SuiteDataStore;
        suiteStore.Add("element-id", "455678");

        // Fetching Value var suiteStore = DataStoreFactory.SuiteDataStore; var
        elementId = (string) suiteStore.Get("element-id");

        // avoid type cast by using generic Get var anotherElementId =
        suiteStore.Get("element-id");

    .. group-tab:: Java

      .. code-block:: java

        // Import Package import
        com.thoughtworks.gauge.datastore.*;

        // Adding value
        DataStore suiteStore = DataStoreFactory.getSuiteDataStore();
        suiteStore.put("element-id", "455678");

        // Fetching value
        DataStore suiteStore = DataStoreFactory.getSuiteDataStore();
        String elementId = (String) suiteStore.get("element-id");

    .. group-tab:: JavaScript

      .. code-block:: javascript

        // Adding value DataStore suiteStore =
        gauge.dataStore.suiteStore.put(key, value);
        // Fetching value DataStore specStore =
        gauge.dataStore.suiteStore.get(key);

    .. group-tab:: Python

      .. code-block:: python

        // Import Package import
        from getgauge.python import DataStoreFactory
        // Adding value DataStore suiteStore =
        DataStoreFactory.suite_data_store().put(key, value)

        // Fetching value DataStore specStore =
        DataStoreFactory.suite_data_store().get(key)

    .. group-tab:: Ruby

      .. code-block:: ruby

        // Adding value
        suite_store = DataStoreFactory.suite_datastore;
        suite_store.put("element-id", "455678");

        // Fetching Value
        suite_store = DataStoreFactory.suite_datastore;
        element_id = suite_store.get("element-id");

Taking Custom Screenshots
-------------------------

-  By default gauge captures the display screen on failure if this
   feature has been enabled.

-  If you need to take CustomScreenshots (using webdriver for example)
   because you need only a part of the screen captured, this can be done
   by **implementing** the ``ICustomScreenshotGrabber`` interface;

.. note::

    If multiple custom ScreenGrabber implementations are found in
    classpath then gauge will pick one randomly to capture the screen.
    This is because Gauge selects the first ScreenGrabber it finds,
    which in turn depends on the order of scanning of the libraries.

.. container:: code-snippet

  .. tabs::

    .. group-tab:: C#

      .. code-block:: java

        //Using Webdriver public
        class CustomScreenGrabber : ICustomScreenshotGrabber {

          // Return a screenshot byte array
          public byte[] TakeScreenshot() {
              var driver = DriverFactory.getDriver();
              return ((ITakesScreenshot) driver).GetScreenshot().AsByteArray;
          }
        }

    .. group-tab:: Java

      .. code-block:: java

        // Using Webdriver public class
        CustomScreenGrabber implements ICustomScreenshotGrabber {
            // Return a screenshot byte array
            public byte[] takeScreenshot() {
                WebDriver driver = DriverFactory.getDriver();
                return ((TakesScreenshot) driver).getScreenshotAs(OutputType.BYTES);
            }

        }

    .. group-tab:: JavaScript

      .. code-block:: javascript

        gauge.screenshotFn = function () {
          return "base64encodedstring";
        };

    .. group-tab:: Python

      .. code-block:: python

        from getgauge.python import screenshot
        @screenshot
        def take_screenshot():
            return "base64encodedstring"

    .. group-tab:: Ruby

      .. code-block:: ruby

        # Using Webdriver
        Gauge.configure do |config|
          # Return a screenshot byte array
          config.screengrabber = -> {
            driver.save_screenshot('/tmp/screenshot.png')
            return File.binread("/tmp/screenshot.png")
          }
        end


.. _reports_custom_messages:

Custom messages in reports
--------------------------

Custom messages/data can be added to execution reports using the below
API from the step implementations or hooks.

These messages will appear under steps in the execution reports.

.. container:: code-snippet

  .. tabs::

    .. group-tab:: C#

      .. code-block:: java

        GaugeMessages.WriteMessage("Custom message for report");
        var id = "4567";
        GaugeMessages.WriteMessage("User id is {0}", id);

    .. group-tab:: Java

      .. code-block:: java

        Gauge.writeMessage("Custom message for report");
        String id = "4567";
        Gauge.writeMessage("User id is %s", id);

    .. group-tab:: JavaScript

      .. code-block:: javascript

        gauge.message("Custom message for report");

    .. group-tab:: Python

      .. code-block:: python

        from getgauge.python import Messages

        Messages.write_message("Custom message for report")

    .. group-tab:: Ruby

      .. code-block:: ruby

        Gauge.write_message("Custom message for report")
        id = "4567"
        Gauge.write_message("User id is" + id)

Enum as Step parameter
----------------------

.. note:: This feature is currently only supported for ``Java``.

The constant values of an Enum data type can be used as parameters to a
Step. However, the type of parameter should match the Enum name itself
in step implementation.

**Step**

.. code-block:: gauge

  * Navigate towards "SOUTH"

**Implementation**

.. code-block:: java
  :caption: Java

  public enum Direction { NORTH, SOUTH, EAST, WEST; }

  @Step("Navigate towards ")
  public void navigate(Direction direction) {
     //  code here
  }

Continue on Failure
-------------------

The default behaviour in Gauge is to break execution on the first
failure in a :ref:`step <step_syntax>`. So, if the
first step in a :ref:`scenario <scenario_syntax>`
fails, the subsequent steps are skipped. While this works for a majority
of use cases, there are times when you need to execute all steps in a
scenario irrespective of whether the previous steps have failed or not.

To address that requirement, Gauge provides a way for language runners
to mark steps as recoverable, depending on whether the step
implementation asks for it explicitly. Each language runner uses
different syntax, depending on the language idioms, to allow a step
implementation to be marked to continue on failure.

.. container:: code-snippet

  .. tabs::

    .. group-tab:: C#

      .. code-block:: java

        // The ``[ContinueOnFailure]`` attribute tells Gauge to continue executing others
        // steps even if the current step fails.

        public class StepImplementation {
            [ContinueOnFailure]
            [Step("Say <greeting> to <product name>")]
            public void HelloWorld(string greeting, string name) {
                // If there is an error here, Gauge will still execute next steps
            }

        }

    .. group-tab:: Java

      .. code-block:: java

        // The ``@ContinueOnFailure`` annotation tells Gauge to continue executing other
        // steps even if the current step fails.

        public class StepImplementation {
            @ContinueOnFailure
            @Step("Say <greeting> to <product name>")
            public void helloWorld(String greeting, String name) {
                // If there is an error here, Gauge will still execute next steps
            }

        }

    .. group-tab:: JavaScript

      .. code-block:: javascript

        // The ``@ContinueOnFailure`` annotation tells Gauge to continue executing other
        // steps even if the current step fails.

        gauge.step("Say <greeting> to <product>.", { continueOnFailure: true}, function (greeting,product) {
        });

    .. group-tab:: Python

      .. code-block:: python

        // The ``@ContinueOnFailure`` annotation tells Gauge to continue executing other
        // steps even if the current step fails.

        @continue_on_failure([RuntimeError])
        @step("Say <greeting> to <product>")
        def step2(greeting,product):
          pass

    .. group-tab:: Ruby

      .. code-block:: ruby

        # The ``:continue_on_failure => true`` keyword argument
        # tells Gauge to continue executing other steps even
        # if the current step fails.

        step 'Say <greeting> to <name>', :continue_on_failure => true do |greeting, name|
          # If there is an error here, Gauge will still execute next steps
        end

Continue on Failure can take an optional parameter to specify the list
of error classes on which it would continue to execute further steps in
case of failure. This is currently supported only with the following runners.

.. code-block:: java
  :caption: Java

  @ContinueOnFailure({AssertionError.class, CustomError.class})
  @Step("hello")
  public void sayHello() {
    // code here
  }

  @ContinueOnFailure(AssertionError.class)
  @Step("hello")
  public void sayHello() {
    // code here
  }

  @ContinueOnFailure
  @Step("hello")
  public void sayHello() {
    // code here
  }

.. code-block:: python
  :caption: Python

  @continue_on_failure([RuntimeError])
  @step("Step 2")
  def step2():
      pass

In case no parameters are passed to ``@ContinueOnFailure``, on any type
of error it continues with execution of further steps by default.

This can be used to control on what type of errors the execution should
continue, instead of just continuing on every type of error. For
instance, on a ``RuntimeException`` it's ideally not expected to
continue further. Whereas if it's an assertion error, it might be fine
to continue execution.

.. note::

  -  Continue on failure comes into play at post execution, i.e. after the step method is executed. If there is a failure in executing the step, ex. parameter count/type mismatch, Gauge will not honour the ``ContinueOnFailure`` flag.
  -  Continue on failure does not apply to :ref:`hooks <execution_hooks>`. Hooks always fail on first error.
  -  Step implementations are still non-recoverable by default and Gauge does not execute subsequent steps upon failure. To make a step implementation continue on failure, it needs to be explicitly marked in the test code.
  -  There is no way to globally mark a test run to treat all steps to continue on failure. Each step implementation has to be marked explicitly.
  -  If an implementation uses step aliases, marking that implementation to continue on failure will also make all the aliases to continue on failure. So, if a step alias is supposed to break on failure and another step alias is supposed to continue on failure, they need to be extracted to two different step implementations.


Step alias
----------

Multiple Step names for the same implementation. The number and type of
parameters for all the steps names must match the number of parameters
on the implementation.

Use case
^^^^^^^^

There may be situations where while authoring the specs, you may want to
express the same functionality in different ways in order to make the
specs more readable.

Example 1
~~~~~~~~~

.. code-block:: gauge

    # User Creation

    ## Multiple Users

    * Create a user "user 1"
    * Verify "user 1" has access to dashboard
    * Create another user "user 2"
    * Verify "user 2" has access to dashboard

In the scenario named Multiple Users, the underlying functionality of
the first and the third step is the same. But the way it is expressed is
different. This helps in conveying the intent and the functionality more
clearly. In such situations like this, step aliases feature should be
used so that you can practice DRY principle at code level, while
ensuring that the functionality is expressed clearly.

Implementation
""""""""""""""

.. container:: code-snippet

  .. tabs::

    .. group-tab:: C#

        .. code-block:: java

            public class Users {

                [Step({"Create a user <user_name>", "Create another user <user_name>"})]
                public void HelloWorld(string user_name) {
                    // create user user_name
                }

            }

    .. group-tab:: Java

        .. code-block:: java

            public class Users {

                @Step({"Create a user <user_name>", "Create another user <user_name>"})
                public void helloWorld(String user_name) {
                    // create user user_name
                }

            }

    .. group-tab:: JavaScript

        .. code-block:: javascript

            step(["Create a user <username>", "Create another user <username>"], function (username) {
            // do cool stuff
            });

    .. group-tab:: Python

        .. code-block:: python

            from getgauge.python import step

            @step(["Create a user <user name>", "Create another user <user name>"])
            def hello(user_name):
                print("create {}.".format(user_name))

    .. group-tab:: Ruby

        .. code-block:: ruby

            step 'Create a user ','Create another user ' do |user_name|
                // create user user_name
            end

Example 2
~~~~~~~~~

.. code-block:: gauge

    ## User Creation

    * User creates a new account
    * A "welcome" email is sent to the user

    ## Shopping Cart

    * User checks out the shopping cart
    * Payment is successfully received
    * An email confirming the "order" is sent

In this case, the underlying functionality of the last step (sending an
email) in both the scenarios is the same. But it is expressed more
clearly with the use of aliases. The underlying step implementation
could be something like this.

Implementation
""""""""""""""
.. container:: code-snippet

  .. tabs::

    .. group-tab:: C#

        .. code-block:: java

            public class Users {

                [Step({"A <email_type> email is sent to the user", "An email confirming the <email_type> is sent"})]
                public void HelloWorld(string email_type) {
                    // Send email of email_type
                }

            }

    .. group-tab:: Java

        .. code-block:: java

            public class Users {

                @Step({"A <email_type> email is sent to the user", "An email confirming the <email_type> is sent"})
                public void helloWorld(String email_type) {
                    // Send email of email_type
                }

            }

    .. group-tab:: JavaScript

        .. code-block:: javascript

            step(["A <email_type> email is sent to the user", "An email confirming the <email_type> is sent"], function (email_type) {
                // do cool stuff
            });

    .. group-tab:: Python

        .. code-block:: python

            from getgauge.python import step

            @step(["A <email_type> email is sent to the user", "An email confirming the <email_type> is sent"])
            def email(email_type):
                print("create {}.".format(email_type))

    .. group-tab:: Ruby

        .. code-block:: ruby

            step 'A email is sent to the user', 'An email confirming the is sent' do |email_type|
                email_service.send email_type
            end
