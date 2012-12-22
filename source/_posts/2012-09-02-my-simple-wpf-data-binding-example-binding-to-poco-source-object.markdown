---
comments: false
date: 2012-09-02 18:25:10
layout: post
slug: my-simple-wpf-data-binding-example-binding-to-poco-source-object
title: My simple WPF data binding example - binding to POCO Source Object
wordpress_id: 161
categories:
- exocortex
---


[xml]
<Window
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:System="clr-namespace:System;assembly=mscorlib" xmlns:local="clr-namespace:BindingExamples" x:Class="BindingExamples.MainWindow"
        Title="MainWindow" Height="350" Width="525"
        >
    <Window.DataContext>
        <local:TheSourceObject/>
    </Window.DataContext>


    <Grid>
        <TextBox Text="{Binding TheChangingProperty, Mode=OneWay}"/>

    </Grid>
</Window>

[/xml]

[csharp]
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Diagnostics;
using System.Linq;
using System.Text;
using System.Threading;
using System.Threading.Tasks;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Data;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Imaging;
using System.Windows.Navigation;
using System.Windows.Shapes;

namespace BindingExamples
{
    /// <summary>
    /// Interaction logic for MainWindow.xaml
    /// </summary>
    public partial class MainWindow : Window
    {
        private TheSourceObject _mySourceObject;

        public MainWindow()
        {
            InitializeComponent();
            _mySourceObject = new TheSourceObject();
            //DataContext = _mySourceObject;
            
        }
    }

    public class TheSourceObject : INotifyPropertyChanged 
    {
        private string _theChangingProperty;
        // has to implement INotifyPropertyChanged

        public TheSourceObject()
        {
            var worker = new BackgroundWorker();
            worker.DoWork += worker_DoWork;
            worker.RunWorkerAsync();

        }

        void worker_DoWork(object sender, DoWorkEventArgs e)
        {
            ChangeProperty();
        }

        public event PropertyChangedEventHandler PropertyChanged;

        protected virtual void OnPropertyChanged(string propertyName)
        {
            PropertyChangedEventHandler handler = PropertyChanged;
            if (handler != null) handler(this, new PropertyChangedEventArgs(propertyName));
        }

        public string TheChangingProperty
        {
            get { return _theChangingProperty;
            }
        }

        void ChangeProperty()
        {
            int count = 0;
            while (count < 100)
            {
                _theChangingProperty = Convert.ToString(count);
                Debug.WriteLine("Changed property to : " + _theChangingProperty);
                OnPropertyChanged("TheChangingProperty");
                Thread.Sleep(2000);
                count++;
            }
        }
    }
}
[/csharp]


