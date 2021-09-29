# Sublayers

Following is an example of how **Sublayers** can be leveraged in a collaborative environment.

For this example, lets assume we have a team of modelers, layout, animators and lighters working on a shot with a character composed of different geometries. For simplicity we will have following hierarchy.

```text

root
  |__SomeCharacter
  |    |__Jacket
  |    |__Legs
  |__Hat
  |    |__Hatgeo
```

In the above example, we will have a primitive named **SomeCharacter**, with two children **body**, **legs** and another primitive named **Hat** with a single child **Hatgeo**. As we will see in the example later, we will be using USD's composition arc in conjunction with specifiers to setup a multi-department scene allowing multiple artists to work on items collaboratively.


Lets create a directory named **someshot**. This will be the root directory for our shot. Next we can create few directories which will be housing our **usd** files later.
```shell
mkdir -p someshot/{model, layout, anim, lighting}
```

Next, we will create a model using the **USD Ascii** format inside the **model** directory.
```shell
touch char.usda
```

Inside our **model/char.usda** file:

```text
#usda 1.0

def Xform "SomeCharacter" (kind="group")
{
    def Sphere "Jacket" (kind="component")
    {
        double radius = 2.5
    }
}
```
