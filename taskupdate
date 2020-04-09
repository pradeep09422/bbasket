package sample;

import java.io.File;
import java.io.FileOutputStream;
import java.io.IOException;
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;

import org.apache.poi.ss.usermodel.Cell;
import org.apache.poi.ss.usermodel.Row;
import org.apache.poi.xssf.usermodel.XSSFSheet;
import org.apache.poi.xssf.usermodel.XSSFWorkbook;
import org.openqa.selenium.By;
import org.openqa.selenium.JavascriptException;
import org.openqa.selenium.JavascriptExecutor;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.interactions.Actions;
import org.openqa.selenium.support.ui.ExpectedConditions;
import org.openqa.selenium.support.ui.WebDriverWait;

public class Bigbasketnew 
{
	
	public void Products() throws IOException 
	{
	WebDriver driver;
	System.setProperty("webdriver.chrome.driver", "F:\\\\selenium\\\\chromedriver.exe"); // Setting system properties of ChromeDriver
	 driver = new ChromeDriver(); //Creating an object of ChromeDriver
	 driver.get("https://www.bigbasket.com/");
	 driver.manage().window().maximize();
	 driver.get("Url");
	 WebDriverWait wait= new WebDriverWait(driver,20);
	 
	 XSSFWorkbook workbook=new XSSFWorkbook();
	 XSSFSheet sheet = workbook.createSheet("Products");
	 
	 Row row=sheet.createRow(0);
	 
	 Cell Brand_Column=row.createCell(0);
	 Brand_Column.setCellValue("Brand Name");
	 
	 Cell Product_Column=row.createCell(1);
	 Product_Column.setCellValue("Product Name");
	 
	 Cell Quantity_Column=row.createCell(2);
	 Quantity_Column.setCellValue("Quantity");
	 
	 Cell Price_Column=row.createCell(3);
	 Price_Column.setCellValue("Price");
	 
	 waitForPageToLoad(driver);
	 Actions focusOnArrow =new Actions(driver);
	 focusOnArrow.moveToElement(driver.findElement(By.xpath("//span[@class='arrow-marker']")));
	 driver.findElement(By.xpath("//span[@class='arrow-marker']")).click();
	 
	 driver.findElement(By.xpath("//div[@class='dropdown-menu latest-ab-bb']/descendant::div[@qa='cityDD']/descendant::div[@placeholder='Select your city']/span")).click();
	 driver.findElement(By.xpath("//div[@class='dropdown-menu latest-ab-bb']/descendant::div[@qa='cityDD']/descendant::input[@type='search']")).sendKeys("Hyd");
	 
	 driver.findElement(By.xpath("//a/span[test()='Hyderabad']")).click();
	 driver.findElement(By.xpath("//div[@classs='dropdownmenu latest-at-bb']/descendant::input[@qa='areaInput']")).sendKeys("");
	 
	 wait.until(ExpectedConditions.visibilityOf(driver.findElement(By.xpath("//button[@qa='continueBtn']"))));
	 driver.findElement(By.xpath("//button[@qa='continueBtn']")).click();
	 
	 waitForPageToLoad(driver);
	 Actions actions = new Actions(driver);
	 //WebElement a=driver.findElement(By.xpath("//a[@qa='categoryDD']"));
	 wait.until(ExpectedConditions.presenceOfElementLocated(By.xpath("//a[@qa='categoryDD']")));
	 actions.moveToElement(driver.findElement(By.xpath("//a[@qa='categoryDD']"))).perform();
	 //actions.moveToElement(a).perform();
	 wait.until(ExpectedConditions.presenceOfElementLocated(By.xpath("//a[@qa='catL1' and text()='Beverages']")));
	 driver.findElement(By.xpath("//a[@qa='catL1' and text()='Beverages']")).click();
	 
	 wait.until(ExpectedConditions.presenceOfAllElementsLocatedBy(By.xpath("//div[@qa='product']")));
	 
	// list to add product details like name,quantity,price etc.
	 List<WebElement> allproducts = driver.findElements(By.xpath("//div(@qa='product']"));
	 //map add to details list
	 HashMap<Integer, List<String>> productMap = new HashMap<Integer, List<String>>();
	 int mapIndex = 1;
	//loop through total product
	for (int productIndex = 1; productIndex <= allproducts.size(); productIndex++){ 
		List<String> productsDetails = new ArrayList<String>();
		//check drop down is available for product
		if (driver.findElements(By.xpath("(//div[@qa='product'])[\" + productIndex + \"]/descendant::button[@data-toggle='dropdown']")).size() > 0)
			{
			driver.findElement(By.xpath("(//div[@qa='product'])[\" + productIndex + \"]/descendant::button[@data-toggle='dropdown']")).click();
			
			driver.findElement(By.xpath("(//div[@qa='product'])[\" + productIndex + \"]/descendant::button[@data-toggle='dropdown']//following-sibling::ul/li[2]))")).click();
		
		productsDetails.add(0,driver.findElement(By.xpath("(//div[@qa='product'])[\" + productIndex + \"]/descendant::div[@qa='product_name']/h6")).getText());
		productsDetails.add(1,driver.findElement(By.xpath("(//div[@qa='product'])[\" + productIndex + \"]/descendant::div[@qa='product_name']/a")).getText());
		
		productsDetails.add(2,driver.findElement(By.xpath("(//div[@qa='product'])[\" + productIndex + \"]/descendant::button[@data-toggle='dropdown']//following-sibling::ul/li[2]/descendant::span[@ng-bind='allProducts.w']))")).getText());	
		productsDetails.add(3,driver.findElement(By.xpath("(//div[@qa='product'])[\" + productIndex + \"]/descendant::button[@data-toggle='dropdown']//following-sibling::ul/li[2]/descendant::span[@ng-bind='allProducts.sp']))")).getText());
		productMap.put(mapIndex,productsDetails);
		mapIndex++;
						
			}
		else
		{
			productsDetails.add(0,driver.findElement(By.xpath("(//div[@qa='product'])[\" + productIndex + \"]/descendant::div[@qa='product_name']/h6")).getText());
			productsDetails.add(1,driver.findElement(By.xpath("(//div[@qa='product'])[\" + productIndex + \"]/descendant::div[@qa='product_name']/a")).getText());
			productsDetails.add(2,driver.findElement(By.xpath("(//div[@qa='product'])[\" +productIndex + \"]/descendant::span[@ng-bind='vm.selectedProduct.w']))")).getText());
			productsDetails.add(3,driver.findElement(By.xpath("(//div[@qa='product'])[\" +productIndex + \"]/descendant::span[@class='discnt-price']/span[contains(@ng-bind,'vm.selectedProduct.sp')]")).getText());
			productMap.put(mapIndex,productsDetails);
			mapIndex++;
		}
	}
	//place product details in excel
	for(Integer Products:productMap.keySet())
	{
		row=sheet.createRow(Products);
		Cell brand=row.createCell(0);
		brand.setCellValue(productMap.get(Products).get(0));
		Cell product = row.createCell(1);
		brand.setCellValue(productMap.get(Products).get(1));
		Cell quantity = row.createCell(2);
		brand.setCellValue(productMap.get(Products).get(2));
		Cell price= row.createCell(3);
		brand.setCellValue(productMap.get(Products).get(3));
		
		}
	//Write product details in to excel
	FileOutputStream productDetailsFile = new FileOutputStream(new File("path of the file"));
	workbook.write(productDetailsFile);
	
}
	private void waitForPageToLoad(WebDriver driver) 
	{
		try{
			for(int i = 0;i<=i;i++)
			{
			if (((JavascriptExecutor) driver).executeScript("return document ready state").equals("complete"))
			{
			break;
			}
			}
		}
			catch (JavascriptException e)
			{
			
			}
		
	}

}
