# ComparatorOCP3

В примере метод sort будет без компаратора и перегруженный метод sort, где в параметр передается компаратор.

Компаратор

Иногда вы хотите отсортировать объект, который не реализован Comparable, или вы хотите отсортировать объекты по-разному в разное время.
Предположим, что мы добавляем weightв наш Duckкласс. Теперь у нас есть следующее:
public class Duck implements Comparable<Duck> { 
  private String name; 
  private int weight; 
  public Duck(String name, int weight) { 
     this.name = name;   
   this.weight = weight;
   } 
  public String getName() {  
return name;
 }  
 public int getWeight() { 
 return weight; 
} 
  public String toString() {
 return name; 
}  
public int compareTo(Duck d) {
      return name.compareTo(d.name); 
  }}
Сам Duckкласс может быть определен compareTo()только одним способом. В этом случае nameбыл выбран. Если мы хотим отсортировать что-то еще, мы должны определить этот порядок сортировки вне compareTo()метода:

public static void main(String[] args) {  
 Comparator<Duck> byWeight = new Comparator<Duck>() { 
     public int compare(Duck d1, Duck d2) {  
       return d1.getWeight()—d2.getWeight(); 
     } 
  };
   List<Duck> ducks = new ArrayList<>();
   ducks.add(new Duck("Quack", 7));
   ducks.add(new Duck("Puddles", 10)); 
  Collections.sort(ducks); 
  System.out.println(ducks);             // [Puddles, Quack]
   Collections.sort(ducks, byWeight); 
  System.out.println(ducks);             // [Quack, Puddles]
}
Сначала мы определили внутренний класс с помощью компаратора. Затем мы отсортировали без компаратора и с компаратором, чтобы увидеть разницу в выходе.
