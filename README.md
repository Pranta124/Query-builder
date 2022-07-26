# Query-builder
 public function slider_2()
    {
        // for slider
        $sliders = Slider::where('status', 1)->where('ecom_id', '2')->orderBy('id', 'DESC')->get(['slider_img']);
        // end slider
        return response()->json([
            'slider' => $sliders
            ]);
    }
     public function dailyBestSales_2()
    {
         $dailyBestSales =  DB::table('order_items')
            ->join('products', 'products.id', '=', 'order_items.product_id')
            ->where('ecom_name','2')
            ->select('product_id', DB::raw('count(*) as total'), 'product_id','product_name','product_descp','product_thambnail','selling_price','discount_price')
            ->groupBy('product_id')
            ->orderBy('total', 'DESC')
            ->limit(18)
            ->get();

            return response()->json([
                'dailyBestSales' =>$dailyBestSales
                ]);
    }
     public function most_popular_all_2()
    {
        $most_popular_all = DB::table('order_items')
            ->join('products', 'products.id', '=', 'order_items.product_id')->where('products.ecom_name','2')
             ->select('product_id', DB::raw('count(*) as total'), 'product_id','products.product_name','products.product_thambnail','products.selling_price','products.discount_price','products.unit')
            ->groupBy('product_id')
            ->orderBy('total', 'DESC')

            ->get();
         return response()->json([
             'most_popular_all'=> $most_popular_all
             ]);
    }
    // for  hot_deals
    public function hot_deals_2()
    {
        //  $hot_deals = DB::table('products')
        //      ->select(DB::raw('id') ,'product_thambnail','product_name','selling_price','discount_price')
        //      ->where('hot_deals', 1)->where('ecom_name', '2')->where('discount_price', '!=', NULL)
        //     ->groupBy('id')
        //     ->orderBy('id', 'DESC')
        //      ->get();
         $hot_deals = Product::with('multiImg')->where('hot_deals', 1)->where('ecom_name', '2')->where('discount_price', '!=', NULL)->select('id','product_thambnail','product_name','selling_price','discount_price','start_date','end_date')->orderBy('id', 'DESC')->limit(6)->get();
        return response()->json([
            'deal of day' => $hot_deals
            ]);
    }
        //banner
    public function banner1_2()
    {
          // home page banner-category
        $banner1 = Banner::where('status', 1)->where('ecom_id', 2)->select(['bennar_img'])->orderBy('id', 'DESC')->first();

        return response()->json([
            'banner1_2' => $banner1,

        ]);

    }
       public function banner2_2()
    {
          // home page banner-category
         $banner2 = Banner::where('status', 1)->where('ecom_id','2')->select(['bennar_img'])->orderBy('id', 'DESC')->first();

        return response()->json([
            'banner2_2' => $banner2,

        ]);

    }
    public function top_selling_2()
    {
          $popular_product =  DB::table('order_items')
            ->join('products', 'products.id', '=', 'order_items.product_id')->where('products.ecom_name','2')
             ->select('product_id', DB::raw('count(*) as total'), 'product_id','products.product_name','products.product_thambnail','products.selling_price','products.discount_price')
            ->groupBy('product_id')
            ->orderBy('total', 'DESC')
            ->limit(6)
            ->get();
            return response()->json([
                'Popular_product' => $popular_product
                ]);
    }
      public function trending_product_2()
    {
          $popular_product =  DB::table('order_items')
            ->join('products', 'products.id', '=', 'order_items.product_id')->where('products.ecom_name','2')
             ->select('product_id', DB::raw('count(*) as total'), 'product_id','products.product_name','products.product_thambnail','products.selling_price','products.discount_price')
            ->groupBy('product_id')
            ->orderBy('total', 'DESC')
            ->limit(6)
            ->get();
            return response()->json([
                'trending_product' => $popular_product
                ]);
    }
    public function top_rated_2()
    {
     $top_rated = DB::table('reviews')
            ->select('products.*', 'brands.brand_name_cats_eye')
            ->join('products', 'product_id', 'products.id')
            ->join('brands', 'products.brand_id', 'brands.id')
            ->distinct('product_id')
            ->where('star', '>', 3)
            ->get();
        return response()->json([
            'top_rated' => $top_rated
            ]);
    }
     public function recently_added_2()
    {
          $latest_products = DB::table('products')
                            ->where('ecom_name','2')
                             ->select(['id','product_thambnail','product_name','selling_price','discount_price'])
                             ->get();

          return response()->json([
              'recently_added' => $latest_products
              ]);
    }
     public function special_offers_2()
    {
        $special_offers = DB::table('products')
                        ->where('ecom_name','2')
                        ->select('id','product_thambnail','product_name','selling_price','discount_price','unit','product_descp')
                        ->get();

        return response()->json([
            'special_offers' => $special_offers
            ]);
    }
    public function related_product_2($cat_id,$subcat_id,$id)
    {
        // dd($id);
            $recomndedProduct = DB::table('products')
            ->where('ecom_name','2')
            ->where('category_id',$cat_id)
            ->where('id', '!=', $id)

            ->orderBy('id','desc')
            ->get(['id','product_thambnail','product_name','selling_price','discount_price']);


        return response()->json([
            'related_product_2'=>$recomndedProduct
        ]);
    }
      public function CategoryView_2()
    {
        $getcategory = DB::table('categories')
                        ->where('ecom_id','2')
                        ->select(['id','category_name','category_image','category_icon'])
                        ->get();

        return response()->json([
            'Category' => $getcategory

        ]);
    }
    public function sidebar_CategoryView_2()
    {
        $getcategory = Category::where('ecom_id','2')->select(['id','category_name','category_icon'])->get();

        return response()->json([
            'getcategory' => $getcategory

        ]);
    }
    public function SubCategoryView_2($cat_id)
    {
        $getsubcategory1 = DB::table('sub_categories')
                        ->where('ecom_id','2')
                        ->where('category_id',$cat_id)
                        ->select(['id','sub_category_name','subcategory_image'])
                        ->get();

        return response()->json([
            'getsubcategory' => $getsubcategory1,


        ]);
    }
      public function sidebar_subcategory_2()
    {
        $subcategory = SubCategory::where('ecom_id','2')->select('id','category_id','sub_category_slug_name')->get();
        return response()->json([
            'subcategory' =>$subcategory
            ]);
    }
    //   public function SubSubCategoryView12($cat_id, $subcat_id)
    // {


    //     $productUnderSubCategory = Product::where('ecom_name','1')->where('sub_category_id',$subcat_id)->where('category_id',$cat_id)->where('sub_sub_category_id', null)->get(['id','product_thambnail','product_name','purchase_qty','selling_price','discount_price','video_link','product_descp','unit','product_color','product_size']);

    //     $getsubsubcategory = SubSubCategory::where('ecom_id','1')->where('subcategory_id', $subcat_id)->where('category_id', $cat_id)->get(['id','subsubcategory_name','subsubcategory_image']);

    //     return response()->json([
    //         'productUnderSubCategory' => $productUnderSubCategory,
    //         'getsubsubcategory' => $getsubsubcategory,

    //     ]);


    // }
      public function SubSubCategroy(Request $request)
    {

        $validator = Validator::make($request->all(),[
            'category_id' => 'required',
            'subcategory_id'=>'required'
            ]);
           if ($validator->fails()) {
            return response([
                'errors' => $validator->messages()
            ]);
        }else{

            $subsub_categories = new SubSubCategory();
            $subsub_categories->subcategory_id = $request->subcategory_id;
            $subsub_categories->category_id = $request->category_id;
            // dd($product->category_id);
            $getsubsubcategory = DB::table('sub_sub_categories')
                                ->where('category_id',$subsub_categories->category_id)
                                ->where('subcategory_id', $subsub_categories->subcategory_id)
                                ->select(['id','subsubcategory_name','subsubcategory_image'])
                                ->get();

            return response()->json([

                'SubSubCategory' => $getsubsubcategory
                ]);
        }
    }
    public function sidebar_SubSubCategroy()
    {

        $subsubcategories = SubSubCategory::where('ecom_id','2')->select('id','category_id','subcategory_id','subsubcategory_slug_name')->get();
        // $productUnderSubCategory = Product::where('ecom_id','1')->get();

        return response()->json([
            'subsubcategories' => $subsubcategories,
            // 'productUnderSubCategory' => $productUnderSubCategory
        ]);
    }

    public function grocery_ProductView(Request $request)
    {
        // dd($request->all());
        $product = new Product();

        if($request->category_id)
        {
            $product=Product::where('ecom_name','2')->where('category_id',$request->category_id)->get(['id','product_name','product_thambnail','selling_price','discount_price','unit','product_qty']);



        }
        else if($request->sub_category_id)
        {
            $product=Product::where('ecom_name','2')->where('sub_category_id',$request->sub_category_id)->get(['id','product_name','product_thambnail','selling_price','discount_price','unit','product_qty']);
            // dd($product);
        }
        else
        {
             $product=Product::where('ecom_name','2')->where('sub_sub_category_id',$request->sub_sub_category_id)->get(['id','product_name','product_thambnail','selling_price','discount_price','unit','product_qty']);
        }



        // dd($product);
        return response()->json([
            'products' => $product
            ]);

    }
       /// Product View With Ajax
      public function ProductViewAjax($id)
      {
          $product = Product::with('category', 'subcategory', 'subsubcategory')->findOrFail($id);
          $review = Review::where('product_id', $id)->get()->first();
          $users = Review::where('product_id', $id)->count();
          $multiimgs =  MultiImg::where('product_id', $id)->limit(6)->get();
          $color = $product->product_color;
          $product_colors = explode(',', $color);
          $size = $product->product_size;
          $product_sizes = explode(',', $size);
          $reviews = review::where('product_id', $product->id)->with('user')->orderBy('id', 'DESC')->get();

          return response([
            'product' => $product,
            'review' => $review,
            'color' => $product_colors,
            'size' => $product_sizes,
            'users' => $users,
            'multiimgs' => $multiimgs,
            'reviews' => $reviews
          ]);
      } // end mathod
    //sub_category


    public function SubSubCategoryView($cat_slug, $subcat_slug)
    {
        $subcat22 = SubCategory::where('sub_category_slug_name', $subcat_slug)->first();
        $subsubcategories = SubSubCategory::where('subcategory_id', $subcat22->id)->with('category', 'subcategory')->get();
        $productUnderSubCategory = Product::where('sub_category_id', $subcat22->id)->where('sub_sub_category_id', null)->get();
        $productUnderSubCategory1 = Product::where('sub_category_id', $subcat22->id)->first();
        $getsubsubcategory1 = Product::where('sub_sub_category_id', $subcat22->id)->select('sub_sub_category_id', 'sub_category_id')->distinct('sub_sub_category_id')->get();

        return response([
            'subsubcategories' => $subsubcategories,
            'productUnderSubCategory' => $productUnderSubCategory,
            'getsubsubcategory1' => $getsubsubcategory1,
            'productUnderSubCategory1' => $productUnderSubCategory1
        ]);
    }
     //////Grocery Start////////////
   public function GroceryCategoryView()
   {
       $getcategory = Category::where('ecom_id',2)->get();
       $newest = $getcategory->pluck('id');
       return response
       ([ 'getcategory'=>$getcategory,
           'newest' =>$newest
       ]);

   }
   public function GrocerySubCategoryView($cat_slug)
   {
       $cat = Category::where('category_slug_name', $cat_slug)->first();
       $getsubcategory1 = SubCategory::where('category_id', $cat->id)->distinct('category_id')->get();
       $getsubcategory = SubCategory::with('category')->where('category_id', $cat->id)->get();
       $newest = SubCategory::where('category_id', $cat->id)->first();
       return response([
           'getsubcategory' => $getsubcategory,
           'getsubcategory1' => $getsubcategory1,
           'newest' => $newest
       ]);
   }

      public function GroceryGetProductView1($cat_slug,$subcat_slug,$subsubcat_slug)
   {
        $subsubcat=SubSubCategory::where('subsubcategory_slug_name',$subsubcat_slug)->first();
       $getproductsub = Product::where('sub_sub_category_id', $subsubcat->id)->with('category','subcategory','subsubcategory')->get();
       $getproductsub1 = Product::where('sub_sub_category_id', $subsubcat->id)->with('category','subcategory','subsubcategory')->first();
       return response([
           'getproductsub' => $getproductsub,
           'getproductsub1' => $getproductsub1,

       ]);

   }

    public function GetFilteredProducts2(Request $request)
   {
           $request->validate([
           'sub_category_id' => 'required',
           'minPrice' => 'required',
           'maxPrice' => 'required'
       ]);

       $querys = Product::where('sub_category_id', $request->sub_category_id)

           ->where(function ($query) use ($request) {
               $query->where(function ($subquery) use ($request) {
                   $subquery->whereBetween('selling_price', [$request->minPrice, $request->maxPrice])
                       ->where('discount_price', '=', 0);
               })
                   ->orWhere(function ($subquery) use ($request) {
                       $subquery->whereBetween('discount_price', [$request->minPrice, $request->maxPrice])
                           ->where('discount_price', '!=', 0);
                   });
           })
           ->get(['id','product_thambnail','product_name','selling_price','discount_price','product_qty','product_stock_alert','unit','product_color','product_size','product_descp','video_link']);
       return response()->json($querys);
   }
