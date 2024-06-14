# PROG-POE-PART3
This is for my PROG POE Assignment 

/ This is all the Required Systems Usages Needed to Run the Windows Applications //

// Link to GitHub Respository Below: //

https://github.com/ST10278170/PROG-POE-PART3/edit/main/README.md

// Link to GitHub Respository Above: //

using System.Text;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Data;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Imaging;
using System.Windows.Navigation;
using System.Windows.Shapes;
using System.Collections.Generic;
using System.Linq;
using System.Security.Cryptography.X509Certificates;
using RecipeManagerWPF;
using System.Numerics;

// Below is the Name of the Project and Showcasing of Public & Private Classes //

namespace RecipeManagerWFS
{
    public partial class MainWindow : Window
    { 
        private List<Recipe> recipes = new List<Recipe>();

        public MainWindow()
        {
        InitializeCompnent();

        }
        
        private void AddRecipe_Click(object sender, RoutedEventArgs e)
        {
            var addRecipeWindow = new AddRecipeWindow(recipes);
                addRecipeWindow.ShowDialog();
        }
        
        private void ListRecipes_Click(object sender, RoutedEventArgs e)
        {
            var listRecipesWindow = new ListRecipesWindow(recipes);
                listRecipesWindow.ShowDialog();
        }
        
        private void ViewRecipe_Click(Object sender, RoutedEventArgs e)
        {
            var viewRecipeWindow = new ViewRecipeWindow(recipes);
                viewRecipeWindow.ShowDialog();
        }

        private void FilterRecipes_Click(Object sender, RoutedEventArgs e)
        {
            var filterRecipesWindow = new FilterRecipesWindow(recipes);
                filterRecipesWindow.ShowDialog();
        }

        private void ClearDate_Click(object sender, RoutedEventArgs e)
        {
            recipes.Clear();
                MessageBox.Show("All Recipe Data has Been Removed");
        }
}
}

    public class Ingredient
    {

    public string Name { get; set; }

    public double Qunantity { get; set; }

    public string Unit {  get; set; }

    public int Calories { get; set; }

    public string FoodGroup { get; set; }

    public Ingredient(string name, double quantity,  string unit, int calories, string foodgroup)
    {
        Name =name;
        Qunantity = quantity;
        Unit = unit;
        Calories = calories;
        FoodGroup = foodgroup;
    }
}

    public class Recipe
    { 
        public string Name { get; set; }

        public List<Ingredient> Ingredients { get; set; }
        
        public List<string> Steps { get; set; }

        public double ScaleFactor { get; private set; } = 1.0;

        public string ImagePath { get; set; } // I will have to address an Image later in the Code Plan //

        public Recipe(string name)
        {
            Name = name;
            Ingredients = new List<Ingredient>();
            Steps = new List<string>();
        }

        public void AddIngredient(Ingredient ingredient)
        {
            Ingredients.Add(ingredient);  
        }

        public void AddStep(string step)
        {
            Steps.Add(step);
        }
        
        public void ScaleRecipe(double factor)
        {
            ScaleFactor = factor;
            foreach (var ingredient in Ingredients)
            {
                ingredient.Qunantity *= factor;
            }
        }
        
        public int CalculateTotalCalories()
        {
            return Ingredients.Sum(ingredient => ingredient.Calories); 
        }
        
        public string DisplayRecipe()
        {
            var result = $"Recipe: {Name}\n\nIngredients:\n";

            foreach (var ingredient in Ingredients)
            {
                result += $"{ingredient.Qunantity} {ingredient.Unit} of {ingredient.Name} ({ingredient.Calories} calories, {ingredient.FoodGroup})\n";
            }
                result += "\nSteps:\n";

            for (int i = 0; i < Steps.Count; i++)
            {
            result += $"{i + 1}. {Steps[i]}\n";
            }
                result += $"\nTotal Calories: {CalculateTotalCalories()}";
                return result ;
        }

        private List<Recipe> recipes = new List<Recipe>();
    
        private void AddRecipe_Click(object sender, RoutedEventArgs e)
        {
            var addRecipeWindow = new AddRecipeWindow(recipes);
                addRecipeWindow.Show();
        }

        private void ListRecipes_Click(object sender, RoutedEventArgs e)
        {   
            var listRecipesWindow = new ListRecipesWindow(recipes);
                listRecipesWindow.Show();
        }
        
        private void ViewRecipe_Click(object sender, RoutedEventArgs e)
        {
            var viewRecipeWindow = new ViewRecipeWindow(recipes);
                viewRecipeWindow.Show();
        }

        private void FilterRecipes_Click(object sender, RoutedEventArgs e)
        {
            var filerRecipesWindow = new FilterRecipesWindow(recipes);
                filerRecipesWindow.Show();
        }
        
        private void ClearDate_Click(object sender, RoutedEventArgs e)
        {
            recipes.Clear();
        MessageBox.Show("All Recipe Data has Been Removed");
    }

  }


