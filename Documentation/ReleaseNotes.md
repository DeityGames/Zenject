
## <a id="release-notes"></a>Release Notes

4.5 (September 1, 2016)
- Fixed DiContainer.ResolveTypeAll() method to properly search in parent containers
- Fixed exception that was occuring with Factories when using derived parameter types
- Fixed FromResolve to properly search in parent containers
- Fixed exception that was occuring with FromMethod when using derived parameter types

4.4 (July 23, 2016)
- Changed the way installers are called from other installers, to allow strongly typed parameter passing
- Added untyped version of FromMethod
- Added FromSiblingComponent bind method
- Added non-generic FromFactory bind method
- Minor bug fix to command binding to work with InheritInSubcontainers() method
- Bug fix - NonLazy method was not working properly when used with ByInstaller or ByMethod

4.3 (June 4, 2016)
- Changed to disallow using null with BindInstance by default, to catch these errors earlier
- Changed to use UnityEngine.Object when referring to prefabs to allow people to get some stronger type checking of prefabs at edit time
- (bug fix) for Hololens with Unity 5.4
- (bug fix) Scene decorator property was not being serialized correctly
- (bug fix) Custom factories were not validating in some cases

4.2 (May 30, 2016)
- Finally updated the documentation
- Renamed FromGetter to FromGetterResolve
- Added some optimizations to convention binding
- Renamed InstallPrefab to InstallPrefabResource
- (bug) Fixed PrefabFactory to work with abstract types
- (bug) Fixed some bugs related to convention binding
- (bug) Fixed bug with Unity 5.3.5 where the list of installers would not serialize properly
- (but) Fixed minor bug with validation

4.1 (May 15, 2016)
- Changed ResolveAll method to be optional by default, so it can return the empty list
- Removed Zenject.Commands namespace in favour of just Zenject
- Added convention based binding (eg. Container.Bind().To(x => x.AllTypes().DerivingFrom()))
- Fixed GameObjectCompositionRoot to expose an optional facade property in its inspector
- Renamed CompositionRoot to Context.
- Changed to just re-use the InjectAttribute instead of PostInjectAttribute
- Better support for making custom Unity EditorWindow implementations that use Zenject
- Added right click Menu items in project pane to create templates of common zenject C# files
- Renamed TestWithContainer to ZenjectUnitTestFixture
- Added simple test framework for both unit tests and integration tests
- Changed Identifier to be type object so it can be used with enums (or other types)
- Added InjectLocal attribute
- Changed to guarantee that any component that is injected into another component has itself been injected already
- Fixed an issue where calling Resolve<> or Instantiate<> inside an installer would cause objects to be injected twice
- Fixes to WSA platform
- Changed to automatically call ScriptableObject.CreateInstance when creating types that derive from ScriptableObject
- Fix to non-unity build

4.0 (April 30, 2016)
- Added another property to CompositionRoot to specify installers as prefabs re #96
- Changed global composition root to be a prefab instead of assembling together a bunch of ScriptableObject assets re #98
- Changed to lookup Zenject Auto Binding components by default, without the need for AutoBindInstaller. Also added new properties such as CompositionRoot, identifier, and made Component a list. Also works now when put underneath GameObjectCompositionRoot's.
- Added ability to pass in multiple types to the Bind() method. This opens up a lot of possibilities including convention-based binding. This also deprecated the use of BindAllInterfacesToSingle in favour of just BindAllInterfaces<>
- Added "WithArguments" bind method, to allow passing arguments directly to the type instead of always using WhenInjectedInto
- Added concept of EditorWindowCompositionRoot to make it easier to use Zenject with editor plugins
- Added "InheritInSubContainers" bind method, to allow having bindings automatically forwarded to sub containers
- Removed the different Exception classes in favour of just one (ZenjectException)
- Added 'AsCached' method as an alternative to 'AsSingle' and 'AsTransient'. AsCached will function like AsTransient except it will only create the object once and thereafter return that value
- Changed some methods that previously used 'params' to explicitly take a list, to avoid common errors
- Cleaned up InjectContext to be easier to work with
- Made significant change to how Factories work. Now there is just one definitive Factory class, and you can change how that factory constructs the object in your installers
- Changed the fluent interface to specify whether the binding is single or transient as a separate method, to avoid the explosion of ToSinglePrefab, ToTransientPrefab, etc. (now it's just ToPrefab)
- Renamed GlobalCompositionRoot to ProjectCompositionRoot and FacadeCompositionRoot to GameObjectCompositionRoot.
- Added more intuitive bindings for creating subcontainers. eg: Container.Bind().ToSubContainerResolve().ByPrefab()
- Added WithGameObjectName and WithGroupName bind methods to prefab or game object related bindings
- Made another big chagne to the fluent interface to avoid having duplicate methods for with Self and Concrete. Now you choose between Container.Bind().ToSelf() and Container.Bind().To(). ToSelf is assumed if unspecified
- Changed Triggers to directly expose the signal event so they can be used as if they are signals
- Added concept of ScriptableObjectInstaller - especially useful for use with settings
- Added ZenjectSceneLoader class to allow additively loading other scenes as children or siblings of existing scene
- Changed scene decorators to work more intuitively with the multi-scene editting features of Unity 5.3+. You can now drag in multiple scenes together, and as long as you use DecoratorCompositionRoot in scenes above a main scene, they will be loaded together.
- Removed IncludeInactive flag. Now always injects into inactive game objects. This was kinda necessary because validation needs to control the active flag
- Removed the concept of one single DependencyRoot in favour of having any number of them, using binding with identifier. Also added NonLazy() bind method to make this very easy
- Added new attribute ZenjectAllowDuringValidation for use with installer setting objects that you need during validation
- Changed validation to occur at runtime to be more robust and less hacky. Now works by adding dummy values to mark which dependencies have successfully been found
- Renamed BindPriority to BindExecutionOrder
- Removed support for binary version of Zenject. This was necessary since Zenject now needs to use some unity defines (eg. UNITY_EDITOR) which doesn't work in DLLs

3.11 (May 15, 2016)
- Bug fix - Calling Resolve<> or Instantiate<> inside an installer was causing the object to be injected twice
- Added StaticCompositionRoot as an even higher level container than ProjectCompositionRoot, for cases where you want to add dependencies directly to the Zenject assembly before Unity even starts up
- Bug fix - loading the same scene multiple times with LoadSceneAdditive was not working
- Fixed compiler errors with Unity 5.4

3.10 (March 26, 2016)
- Fixed to actually support Windows Store platform
- Added pause/resume methods to TickableManager
- Bug fix - OnlyInjectWhenActive flag did not work on root inactive game objects 

3.9 (Feb 7, 2016)
- Added a lot more error checking when using the ToSingle bindings. It will no longer allow mixing different ToSingle types
- Fixed ToSingleGameObject and ToSingleMonoBehaviour to allow multiple bindings to the same result
- Made it easier to construct SceneCompositionRoot objects dynamically
- Added untyped versions of BindIFactory.ToFactory method
- Removed the ability warn on missing ITickable/IInitializable bindings
- Added a bunch of integration tests
- Reorganized folder structure

3.8 (Feb 4, 2016)
- Changed back to only initializing the ProjectCompositionRoot when starting a scene with a SceneCompositionRoot rather than always starting it in every scene

3.7 (Jan 31, 2016)
- Changed to not bother parenting transforms to the CompositionRoot object by default (This is still optional with a checkbox however)
- Added string parameter to BindMonoBehaviourFactory method to allow specifying the name of an empty GameObject to use for organization
- Changed FacadeFactory to inherit from IFactory
- Changed ProjectCompositionRoot to initialize using Unity's new [RuntimeInitializeOnLoadMethod] attribute
- Added easier ability to validate specific scenes from the command line outside of Unity
- Added AutoBindInstaller class and ZenjectBinding attribute to make it easier to add MonoBehaviours that start in the scene to the container
- Added optional parameter to the [Inject] attribute to specify which container to retrieve from in the case of nested containers
- Fixed some unity-specific bind commands to play more nicely with interfaces

3.6 (Jan 24, 2016)
- Another change to signals to not require parameter types to the bind methods

3.5 (Jan 17, 2016)
- Made breaking change to require separate bind commands for signals and triggers, to allow adding different conditionals on each.

3.4 (Jan 7, 2016)
- Cleaned up directory structure
- Fixed bug with Global bindings not getting their Tick() called in the correct order
- Fixes to the releases automation scripts

3.2 (December 20, 2015)
- Added the concept of "Commands" and "Signals".  See documentation for details.
- Fixed validation for decorator scenes that open decorator scenes.
- Changed to be more strict when using a combination of differents kinds of ToSingle<>, since there should only be one way to create the singleton.
- Added ToSingleFactory bind method, for cases where you have complex construction requirements and don't want to use ToSingleMethod
- Removed the InjectFullScene flag on SceneCompositionRoot.  Now always injects on the full scene.
- Renamed AllowNullBindings to IsValidating so it can be used for other kinds of validation-only logic
- Renamed BinderUntyped to UntypedBinder and BinderGeneric to GenericBinder
- Added the ability to install MonoInstaller's directly from inside other installers by calling Container.Install<MyCustomMonoInstaller>().  In this case it tries to load a prefab from Resources/Installers/MyCustomMonoInstaller.prefab before giving up.  This can be helpful to keep scenes incredibly small instead of having many installer prefabs.
- Added the ability to install MonoInstaller's directly from inside other installers.  In this case it tries to load a prefab from the resources directory before giving up.
- Added some better error output in a few places
- Fixed some iOS AOT issues
- Added BindFacade<> method to DiContainer, to allow creating nested containers without needing to use a factory.
- Added an Open button in scene decorator comp root for easily jumping to the decorated scene
- Removed support for object graph visualization since I hadn't bothered maintaining it
- Got the optional Moq extension method ToMock() working again
- Fixed scene decorators to play more nicely with Unity's own way of handling LoadLevelAdditive.  Decorated scenes are now organized in the scene heirarchy under scene headings just like when calling LoadLevelAdditive normally

3.1
- Changes related to upgrading to Unity 5.3
- Fixed again to make zero heap allocations per frame

3.0
- Added much better support for nested containers.  It now works more closely to what you might expect:  Any parent dependencies are always inherited in sub-containers, even for optional injectables.  Also removed BindScope and FallbackContainer since these were really just workarounds for this feature missing.  Also added [InjectLocal] attribute for cases where you want to inject dependencies only from the local container.
- Changed the way execution order is specified in the installers.  Now the order for Initialize / Tick / Dispose are all given by one property similar to how unity does it, using ExecutionOrderInstaller
- Added ability to pass arguments to Container.Install<>
- Added support for using Facade pattern in combination with nested containers to allow easily created distinct 'islands' of dependencies.  See documentation for details
- Changed validation to be executed on DiContainer instead of through BindingValidator for ease of use
- Added automatic support for WebGL by marking constructors as [Inject]

2.8
* Fixed to properly use explicit default parameter values in Constructor/PostInject methods.  For eg: public Foo(int bar = 5) should consider bar to be optional and use 5 if not resolved.

2.7
* Bug fix to ensure global composition root always gets initialized before the scene composition root
* Changed scene decorators to use LoadLevelAdditive instead of LoadLevel to allow more complex setups involving potentially several decorators within decorators

2.6
* Added new bind methods: ToResource, ToTransientPrefabResource, ToSinglePrefabResource
* Added ability to have multiple sets of global installers
* Fixed support for using zenject with .NET 4.5
* Created abstract base class CompositionRoot for both SceneCompositionRoot and ProjectCompositionRoot
* Better support for using the same DiContainer from multiple threads
* Added back custom list inspector handler to make it easier to re-arrange etc.
* Removed the extension methods on DiContainer to avoid a gotcha that occurs when not including 'using Zenject
* Changed to allow having a null root transform given to DiContainer
* Changed to assume any parameters with hard coded default values (eg: int x = 5) are InjectOptional
* Fixed bug with asteroids project which was causing exceptions to be thrown on the second run due to the use of tags

2.5
* Added support for circular dependencies in the PostInject method or as fields (just not constructor parameters)
* Fixed issue with identifiers that was occurring when having both [Inject] and [InjectOptional] attributes on a field/constructor parameter.  Now requires that only one be set
* Removed BindValue in favour of just using Bind for both reference and value types for simplicity
* Removed GameObjectInstantiator class since it was pretty awkward and confusing.  Moved methods directly into IInstantiator/DiContainer.  See IInstantiator class.
* Extracted IResolver and IBinder interfaces from DiContainer

2.4
* Refactored the way IFactory is used to be a lot cleaner. It now uses a kind of fluent syntax through its own bind method BindIFactory<>

2.3
* Added "ParentContexts" property to InjectContext, to allow very complex conditional bindings that involve potentially several identifiers, etc.
* Removed InjectionHelper class and moved methods into DiContainer to simplify API and also to be more discoverable
* Added ability to build dlls for use in outside unity from the assembly build solution

2.2
* Changed the way installers invoke other installers.  Previously you would Bind them to IInstaller and now you call Container.Install<MyInstaller> instead.  This is better because it allows you to immediately call Rebind<> afterwards

2.1
* Simplified interface a bit more by moving more methods into DiContainer such as Inject and Instantiate.  Moved all helper methods into extension methods for readability. Deleted FieldsInjector and Instantiator classes as part of this
* Renamed DiContainer.To() method to ToInstance since I had witnessed some confusion with it for new users.  Did the same with ToSingleInstance
* Added support for using Zenject outside of Unity by building with the ZEN_NOT_UNITY3D define set
* Bug fix - Validation was not working in some cases for prefabs.
* Renamed some of the parameters in InjectContext for better understandability.
* Renamed DiContainer.ResolveMany to DiContainer.ResolveAll
* Added 'InjectFullScene' flag to CompositionRoot to allow injecting across the entire unity scene instead of just objects underneath the CompositionRoot

2.0

* Added ability to inject dependencies via parameters to the [PostInject] method just like it does with constructors.  Especially useful for MonoBehaviours.
* Fixed the order that [PostInject] methods are called in for prefabs
* Changed singletons created via ToSinglePrefab to identify based on identifier and prefab and not component type. This allows things like ToSingle<Foo>(prefab1) and ToSingle<Bar>(prefab1) to use the same prefab, so you can map singletons to multiple components on the same prefab. This also works with interfaces.
* Removed '.As()' method in favour of specifying the identifier in the first Bind() statement
* Changed identifiers to be strings instead of object to avoid accidental usage
* Renamed ToSingle(obj) to ToSingleInstance to avoid conflict with specifying an identifier
* Fixed validation to work properly for ToSinglePrefab
* Changed to allow using conditions to override a default binding. When multiple providers are found it will now try and use the one with conditions.  So for example you can define a default with `Container.Bind<IFoo>().ToSingle<Foo1>()` and then override for specific classes with `Container.Bind<IFoo>().ToSingle<Foo2>().WhenInjectedInto<Bar>()`, etc.

1.19

* Upgraded to Unity 5
* Added an optional identifier to InjectOptional attribute
* Changed the way priorities are interpreted for tickables, disposables, etc. Zero is now used as default for any unspecified priorities.  This is helpful because it allows you to choose priorities that occur either before or after the unspecified priorities.
* Added some helper methods to ZenEditorUtil for use by CI servers to validate all scenes

1.18

* Added minor optimizations to reduce per-frame allocation to zero
* Fixed unit tests to be compatible with unity test tools
* Minor bug fix with scene decorators, GameObjectInstantiator.

1.17

* Bug fix.  Was not forwarding parameters correctly when instantiating objects from prefabs

1.16

* Removed the word 'ModestTree' from namespaces since Zenject is open source and not proprietary to the company ModestTree.

1.15

* Fixed bug with ToSinglePrefab which was causing it to create multiple instances when used in different bindings.

1.14

* Added flag to CompositionRoot for whether to inject into inactive game objects or ignore them completely
* Added BindAllInterfacesToSingle method to DiContainer
* Changed to call PostInject[] on children first when instantiating from prefab
* Added ILateTickable interface, which works just like ITickable or IFixedTickable for unity's LateUpdate event
* Added support for 'decorators', which can be used to add dependencies to another scene

1.13

* Minor bug fix to global composition root.  Also fixed a few compiler warnings.

1.12

* Added Rebind<> method
* Changed Factories to use strongly typed parameters by default.  Also added ability to pass in null values as arguments as well as multiple instances of the same type
* Renamed _container to Container in the installers
* Added support for Global Composition Root to allow project-wide installers/bindings
* Added DiContainer.ToSingleMonoBehaviour method
* Changed to always include the StandardUnityInstaller in the CompositionRoot class.
* Changed TickableManager to not be a monobehaviour and receive its update from the UnityDependencyRoot instead
* Added IFixedTickable class to support unity FixedUpdate method

1.11

* Removed Fasterflect library to keep Zenject nice and lightweight (it was also causing issues on WP8)
* Fixed bug related to singletons + object graph validation. Changed the way IDisposables are handled to be closer to the way IInitializable and ITickable are handled. Added method to BinderUntyped.

1.10

* Added custom editor for the Installers property of CompositionRoot to make re-ordering easier

1.09

* Added support for nested containers
* Added ability to execute bind commands using Type objects rather than a generic type
* Changed the way IDisposable bindings work to be similar to how ITickable and IInitializable work
* Bug fixes

1.08

* Order of magnitude speed improvement by using more caching
* Minor change to API to use the As() method to specify identifiers
* Bug fixes

1.07

* Simplified API by removing the concept of modules in favour of just having installers instead (and add support for installers installing other installers)
* Bug fixes

1.06

* Introduced concept of scene installer, renamed installers 'modules'
* Bug fixes
