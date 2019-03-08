spring bean的Scope

 Spring容器最初提供了两种bean的scope类型：singleton和prototype,但发布2.0以后，又引入了另外三种scope类型：request、session和global session,这三种只能在web 应用中才可以使用。

    ①singleton：一个Spring容器只有一个Bean实例，此为Spring的默认配置。@Scope("Singleton")
    ②prototype：每次调用新建一个Bean的实例
    ③request：Web项目中，给每个http Request新建一个Bean实例
    ④session：Web项目中，给每个http session新建一个Bean实例
    ⑤globalSession：这个旨在portal应用中有用，给每个global http session新建一个Bean实例
    另外在Spring Batch中还有一个Scope是使用@StepScope，在批处理中使用。
