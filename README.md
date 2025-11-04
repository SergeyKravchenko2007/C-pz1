# C-pz1
using System;
using System.Collections.Generic;
using System.Linq;

public abstract class LibraryItem
{
    public string Name { get; set; }
    public string Id { get; set; }
    public bool IsFree { get; set; } = true;
}

public class Book : LibraryItem
{
    public string Author { get; set; }
}

public class Magazine : LibraryItem
{
    public int Number { get; set; }
}

public class LibraryService
{
    private List<LibraryItem> _items = new List<LibraryItem>();

    public void Add(LibraryItem item)
    {
        _items.Add(item);
    }

    public void Take(string id)
    {
        var item = _items.FirstOrDefault(i => i.Id == id);
        if (item != null && item.IsFree)
        {
            item.IsFree = false;
        }
    }

    public void Return(string id)
    {
        var item = _items.FirstOrDefault(i => i.Id == id);
        if (item != null)
        {
            item.IsFree = true;
        }
    }

    public void ShowFree()
    {
        foreach (var item in _items.Where(i => i.IsFree))
        {
            Console.WriteLine($"{item.Name} ({item.Id})");
        }
    }
}

class Program
{
    static void Main()
    {
        var library = new LibraryService();

        var book = new Book { Name = "Кобзар", Id = "1", Author = "Шевченко" };
        var magazine = new Magazine { Name = "Forbes", Id = "2", Number = 5 };

        library.Add(book);
        library.Add(magazine);

        library.Take("1");
        library.Return("1");
        library.ShowFree();
    }
}
