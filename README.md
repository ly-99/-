package cn.ly;

import org.jboss.arquillian.container.test.api.Deployment;
import org.jboss.arquillian.junit.Arquillian;
import org.jboss.shrinkwrap.api.ShrinkWrap;
import org.jboss.shrinkwrap.api.asset.EmptyAsset;
import org.jboss.shrinkwrap.api.spec.JavaArchive;
import org.junit.runner.RunWith;

import static org.junit.Assert.*;

@RunWith(Arquillian.class)
public class SeleniumBingTest {
    @Deployment
    public static JavaArchive createDeployment() {
        return ShrinkWrap.create(JavaArchive.class)
                .addClass(SeleniumBing.class)
                .addAsManifestResource(EmptyAsset.INSTANCE, "beans.xml");
    }

    public static WebDriver driver = null;
    public static String url="https://cn.bing.com/";

    @org.junit.Before
    public void setUp() throws Exception {
        System.setProperty("webdriver.ie.driver","D:/Tools/IEDriverServer.exe");
        driver = new InternetExplorerDriver();
        driver.get(url);
    }

    @org.junit.After
    public void tearDown() throws Exception {
        driver.quit();
    }

    @org.junit.Test
    public void TestTitle(){
        Assert.assertEquals("微软 Bing 搜索 - 国内版",driver.getTitle());
        WebElement element = driver.findElement(By.id("sb_form_q"));
        element.sendKeys("software");
        element.submit();
    }

    @org.junit.Test
    public void TestXpath(){
        WebElement element = driver.findElement(By.xpath("//*[@id=\"sb_form_q\"]"));
        element.sendKeys("software");
        element.submit();
    }

}
