---
bookToc: false
---



# StringTemplate 工具类

```java

import freemarker.cache.StringTemplateLoader;
import freemarker.template.Configuration;
import freemarker.template.Template;
import freemarker.template.TemplateException;
import lombok.extern.slf4j.Slf4j;

import java.io.IOException;
import java.io.StringWriter;

@Slf4j
public class FreeMarkerTool {

    private static final Configuration CONF = new Configuration(Configuration.VERSION_2_3_21);

    static {
        CONF.setDefaultEncoding("UTF-8");
        CONF.setLogTemplateExceptions(true);
        CONF.setTemplateLoader(new StringTemplateLoader());
    }

    /**
     * @param data            模版数据
     * @param templateContent 模版内容
     */
    public static String process(Object data, String templateContent) throws TemplateException, IOException {

        String name = tplKey(templateContent);

        StringTemplateLoader templateLoader = (StringTemplateLoader) CONF.getTemplateLoader();
        if (null == templateLoader.findTemplateSource(name)) {
            templateLoader.putTemplate(name, templateContent);
        }


        try (StringWriter writer = new StringWriter()) {
            Template template = CONF.getTemplate(name);
            template.process(data, writer);
            return writer.toString();
        }
    }

    private static String tplKey(String ftlContent) {
        return String.valueOf(ftlContent.hashCode());
    }

}
```

## Read More

- [程序开发指南](http://www.kerneler.com/freemarker2.3.23/pgui.html)

