---
layout: post
title: "entityframework.relationship"
description: ""
category: 
tags: []
---
{% include JB/setup %}

# one to one and one to many

    {% highlight ruby %}
    public class user
    {
        public user()
        {
            this.deps = new List<dep>();
        }

        public int id { get; set; }
        public string code { get; set; }
        public string name { get; set; }
        public virtual ICollection<dep> deps { get; set; }
        public virtual dep dep { get; set; }
        public virtual dep dep1 { get; set; }
    }

    public class dep
    {
        public int id { get; set; }
        public Nullable<int> mainUser { get; set; }
        public Nullable<int> secondUser { get; set; }
        public virtual user user { get; set; }
        public virtual user user1 { get; set; }
        public virtual user user2 { get; set; }
    }


    // Relationships
    this.HasOptional(t => t.user)//可空
        .WithMany(t => t.deps)//两边都有导航
        //.WithOptionalDependent(t=>t.dep)如果是1对1
        .HasForeignKey(d => d.mainUser).WillCascadeOnDelete(false);
    this.HasRequired(t => t.user1)
        .WithRequiredPrincipal(t => t.dep)//1对1 外键在user表上 且 不能为空
        .WillCascadeOnDelete(false);

    this.HasOptional(d => d.user2)
        .WithOptionalDependent(t => t.dep1)//1对1 外键在dep表上 可空
        .WillCascadeOnDelete(false);

    {% endhighlight %}
